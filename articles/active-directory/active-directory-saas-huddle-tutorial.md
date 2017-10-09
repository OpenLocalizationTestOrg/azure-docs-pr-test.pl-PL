---
title: "Samouczek: Integracji Azure Active Directory z zbijają się | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i zbijają się."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 0b2f6c4d839943cdd07699a1ff95dc8f90505699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a><span data-ttu-id="409f0-103">Samouczek: Integracji Azure Active Directory z zbijają się</span><span class="sxs-lookup"><span data-stu-id="409f0-103">Tutorial: Azure Active Directory integration with Huddle</span></span>

<span data-ttu-id="409f0-104">Z tego samouczka, dowiesz się, jak toointegrate zbijają się w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="409f0-104">In this tutorial, you learn how toointegrate Huddle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="409f0-105">Integrowanie zbijają się z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="409f0-105">Integrating Huddle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="409f0-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooHuddle</span><span class="sxs-lookup"><span data-stu-id="409f0-106">You can control in Azure AD who has access tooHuddle</span></span>
- <span data-ttu-id="409f0-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooHuddle (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="409f0-107">You can enable your users tooautomatically get signed-on tooHuddle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="409f0-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="409f0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="409f0-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="409f0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="409f0-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="409f0-110">Prerequisites</span></span>

<span data-ttu-id="409f0-111">Integracja tooconfigure usługi Azure AD z zbijają się, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="409f0-111">tooconfigure Azure AD integration with Huddle, you need hello following items:</span></span>

- <span data-ttu-id="409f0-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="409f0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="409f0-113">Zbijają się logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="409f0-113">A Huddle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="409f0-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="409f0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="409f0-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="409f0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="409f0-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="409f0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="409f0-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="409f0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="409f0-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="409f0-118">Scenario description</span></span>

<span data-ttu-id="409f0-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="409f0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="409f0-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="409f0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="409f0-121">Dodawanie zbijają się z galerii hello</span><span class="sxs-lookup"><span data-stu-id="409f0-121">Adding Huddle from hello gallery</span></span>
2. <span data-ttu-id="409f0-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="409f0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-huddle-from-hello-gallery"></a><span data-ttu-id="409f0-123">Dodawanie zbijają się z galerii hello</span><span class="sxs-lookup"><span data-stu-id="409f0-123">Adding Huddle from hello gallery</span></span>
<span data-ttu-id="409f0-124">integracji hello tooconfigure zbijają się do usługi Azure AD, należy tooadd zbijają się z listą tooyour galerii hello zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="409f0-124">tooconfigure hello integration of Huddle into Azure AD, you need tooadd Huddle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="409f0-125">**tooadd zbijają się z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="409f0-125">**tooadd Huddle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="409f0-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="409f0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="409f0-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="409f0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="409f0-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="409f0-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="409f0-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="409f0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="409f0-133">W polu wyszukiwania hello wpisz **zbijają się**.</span><span class="sxs-lookup"><span data-stu-id="409f0-133">In hello search box, type **Huddle**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_search.png)

5. <span data-ttu-id="409f0-135">W panelu wyników hello, wybierz **zbijają się**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="409f0-135">In hello results panel, select **Huddle**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="409f0-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="409f0-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="409f0-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z zbijają się na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="409f0-138">In this section, you configure and test Azure AD single sign-on with Huddle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="409f0-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w zbijają się jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="409f0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Huddle is tooa user in Azure AD.</span></span> <span data-ttu-id="409f0-140">Innymi słowy link relację między użytkownika usługi Azure AD i użytkownikowi hello w zbijają się potrzeb toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="409f0-140">In other words, a link relationship between an Azure AD user and hello related user in Huddle needs toobe established.</span></span>

<span data-ttu-id="409f0-141">W zbijają się, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="409f0-141">In Huddle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="409f0-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z zbijają się, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="409f0-142">tooconfigure and test Azure AD single sign-on with Huddle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="409f0-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="409f0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>

2. <span data-ttu-id="409f0-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="409f0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>

3. <span data-ttu-id="409f0-145">**[Tworzenie użytkownika testowego zbijają się](#creating-a-huddle-test-user)**  -toohave odpowiednikiem Simona Britta w zbijają się, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="409f0-145">**[Creating a Huddle test user](#creating-a-huddle-test-user)** - toohave a counterpart of Britta Simon in Huddle that is linked toohello Azure AD representation of user.</span></span>

4. <span data-ttu-id="409f0-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="409f0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>

5. <span data-ttu-id="409f0-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="409f0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="409f0-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="409f0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="409f0-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji zbijają się.</span><span class="sxs-lookup"><span data-stu-id="409f0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Huddle application.</span></span>

<span data-ttu-id="409f0-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z zbijają się, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="409f0-150">**tooconfigure Azure AD single sign-on with Huddle, perform hello following steps:**</span></span>

1. <span data-ttu-id="409f0-151">W portalu Azure na powitania hello **zbijają się** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="409f0-151">In hello Azure portal, on hello **Huddle** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="409f0-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="409f0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_samlbase.png)

3. <span data-ttu-id="409f0-155">Na powitania **zbijają się w domenie i adresy URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="409f0-155">On hello **Huddle Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_url.png)

    <span data-ttu-id="409f0-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`http://<company name>.huddle.com`</span><span class="sxs-lookup"><span data-stu-id="409f0-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<company name>.huddle.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="409f0-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="409f0-158">This value is not real.</span></span> <span data-ttu-id="409f0-159">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="409f0-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="409f0-160">Skontaktuj się z [klienta zbijają się z pomocą techniczną](https://huddle.zendesk.com) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="409f0-160">Contact [Huddle Client support team](https://huddle.zendesk.com) tooget this value.</span></span> 

4. <span data-ttu-id="409f0-161">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="409f0-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_certificate.png) 

5. <span data-ttu-id="409f0-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="409f0-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-huddle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="409f0-165">Na powitania **zbijają się konfiguracji** kliknij **skonfigurować zbijają się** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="409f0-165">On hello **Huddle Configuration** section, click **Configure Huddle** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="409f0-166">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="409f0-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_configure.png) 
    
7. <span data-ttu-id="409f0-168">tooconfigure rejestracji jednokrotnej zbijają się strony, należy pobrać hello toosend **certyfikatu**, **SAML pojedynczy znak na adres URL usługi**, i **identyfikator jednostki SAML** zbyt[Klienta zbijają się z pomocą techniczną](https://huddle.zendesk.com).</span><span class="sxs-lookup"><span data-stu-id="409f0-168">tooconfigure single sign-on on Huddle side, you need toosend hello downloaded  **Certificate**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** too[Huddle Client support team](https://huddle.zendesk.com).</span></span> <span data-ttu-id="409f0-169">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="409f0-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>  
   
    >[!NOTE]
    > <span data-ttu-id="409f0-170">Logowanie jednokrotne wymaga toobe włączane przez hello zbijają się z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="409f0-170">Single sign-on needs toobe enabled by hello Huddle support team.</span></span> <span data-ttu-id="409f0-171">Otrzymasz powiadomienie po zakończeniu konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="409f0-171">You get a notification when hello configuration has been completed.</span></span> 
    > 

> [!TIP]
> <span data-ttu-id="409f0-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="409f0-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="409f0-173">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="409f0-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="409f0-174">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="409f0-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
   
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="409f0-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="409f0-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="409f0-176">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="409f0-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="409f0-178">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="409f0-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="409f0-179">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="409f0-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="409f0-181">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="409f0-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="409f0-183">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="409f0-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="409f0-185">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="409f0-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="409f0-187">a.</span><span class="sxs-lookup"><span data-stu-id="409f0-187">a.</span></span> <span data-ttu-id="409f0-188">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="409f0-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="409f0-189">b.</span><span class="sxs-lookup"><span data-stu-id="409f0-189">b.</span></span> <span data-ttu-id="409f0-190">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="409f0-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="409f0-191">c.</span><span class="sxs-lookup"><span data-stu-id="409f0-191">c.</span></span> <span data-ttu-id="409f0-192">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="409f0-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="409f0-193">d.</span><span class="sxs-lookup"><span data-stu-id="409f0-193">d.</span></span> <span data-ttu-id="409f0-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="409f0-194">Click **Create**.</span></span>
 
### <a name="creating-a-huddle-test-user"></a><span data-ttu-id="409f0-195">Tworzenie użytkownika testowego zbijają się</span><span class="sxs-lookup"><span data-stu-id="409f0-195">Creating a Huddle test user</span></span>

<span data-ttu-id="409f0-196">toolog użytkowników tooenable usługi Azure AD w tooHuddle, muszą mieć przydzielone do zbijają się.</span><span class="sxs-lookup"><span data-stu-id="409f0-196">tooenable Azure AD users toolog in tooHuddle, they must be provisioned into Huddle.</span></span> <span data-ttu-id="409f0-197">W przypadku hello zbijają się inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="409f0-197">In hello case of Huddle, provisioning is a manual task.</span></span>

<span data-ttu-id="409f0-198">**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="409f0-198">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="409f0-199">Zaloguj się za tooyour **zbijają się** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="409f0-199">Log in tooyour **Huddle** company site as administrator.</span></span>
2. <span data-ttu-id="409f0-200">Kliknij przycisk **obszaru roboczego**.</span><span class="sxs-lookup"><span data-stu-id="409f0-200">Click **Workspace**.</span></span>
3. <span data-ttu-id="409f0-201">Kliknij przycisk **osób \> Zaproś inne osoby**.</span><span class="sxs-lookup"><span data-stu-id="409f0-201">Click **People \> Invite People**.</span></span>
   
   <span data-ttu-id="409f0-202">![Osoby](./media/active-directory-saas-huddle-tutorial/IC787838.png "osób")</span><span class="sxs-lookup"><span data-stu-id="409f0-202">![People](./media/active-directory-saas-huddle-tutorial/IC787838.png "People")</span></span>

4. <span data-ttu-id="409f0-203">W hello **utworzyć nowe zaproszenie** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="409f0-203">In hello **Create a new invitation** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="409f0-204">![Nowe zaproszenie](./media/active-directory-saas-huddle-tutorial/IC787839.png "nowe zaproszenie")</span><span class="sxs-lookup"><span data-stu-id="409f0-204">![New Invitation](./media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span></span>
   
   <span data-ttu-id="409f0-205">a.</span><span class="sxs-lookup"><span data-stu-id="409f0-205">a.</span></span> <span data-ttu-id="409f0-206">W hello **wybierz zespół tooinvite osób toojoin** listy, wybierz **zespołu**.</span><span class="sxs-lookup"><span data-stu-id="409f0-206">In hello **Choose a team tooinvite people toojoin** list, select **team**.</span></span>

   <span data-ttu-id="409f0-207">b.</span><span class="sxs-lookup"><span data-stu-id="409f0-207">b.</span></span> <span data-ttu-id="409f0-208">Hello typu **adres E-mail** prawidłowe usługi Azure AD konta ma zbyt tooprovision**wprowadź adres e-mail dla osób, które chcesz tooinvite** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="409f0-208">Type hello **Email Address** of a valid Azure AD account you want tooprovision in too**Enter email address for people you'd like tooinvite** textbox.</span></span>

   <span data-ttu-id="409f0-209">c.</span><span class="sxs-lookup"><span data-stu-id="409f0-209">c.</span></span> <span data-ttu-id="409f0-210">Kliknij przycisk **zaprosić**.</span><span class="sxs-lookup"><span data-stu-id="409f0-210">Click **Invite**.</span></span>   
   
    >[!NOTE]
    > <span data-ttu-id="409f0-211">Witaj konto usługi Azure AD, czy symbol zastępczy zostanie wysłana wiadomość e-mail, zanim staje się aktywny w tym kontem hello tooconfirm łącza.</span><span class="sxs-lookup"><span data-stu-id="409f0-211">hello Azure AD account holder will receive an email including a link tooconfirm hello account before it becomes active.</span></span> 
    > 

>[!NOTE]
><span data-ttu-id="409f0-212">Możesz użyć innych zbijają się użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision zbijają się konta użytkowników usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="409f0-212">You can use any other Huddle user account creation tools or APIs provided by Huddle tooprovision Azure AD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="409f0-213">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="409f0-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="409f0-214">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooHuddle.</span><span class="sxs-lookup"><span data-stu-id="409f0-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHuddle.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="409f0-216">**tooassign tooHuddle Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="409f0-216">**tooassign Britta Simon tooHuddle, perform hello following steps:**</span></span>

1. <span data-ttu-id="409f0-217">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="409f0-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="409f0-219">Z listy aplikacji hello wybierz **zbijają się**.</span><span class="sxs-lookup"><span data-stu-id="409f0-219">In hello applications list, select **Huddle**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_app.png) 

3. <span data-ttu-id="409f0-221">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="409f0-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="409f0-223">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="409f0-223">Click **Add** button.</span></span> <span data-ttu-id="409f0-224">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="409f0-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="409f0-226">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="409f0-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="409f0-227">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="409f0-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="409f0-228">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="409f0-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="409f0-229">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="409f0-229">Testing single sign-on</span></span>

<span data-ttu-id="409f0-230">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="409f0-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="409f0-231">Po kliknięciu kafelka zbijają się hello w hello Panel dostępu, należy uzyskać automatycznie strony logowania zbijają się w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="409f0-231">When you click hello Huddle tile in hello Access Panel, you should get automatically login page of Huddle application.</span></span>
<span data-ttu-id="409f0-232">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="409f0-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="409f0-233">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="409f0-233">Additional resources</span></span>

* [<span data-ttu-id="409f0-234">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="409f0-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="409f0-235">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="409f0-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_203.png
