---
title: 'Samouczek: Integracji Azure Active Directory z Nexonia | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Nexonia."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a93b771a-9bc3-444a-bdc0-457f8bb7e780
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/1/2017
ms.author: jeedes
ms.openlocfilehash: 3778804084a7989414260bae5654cf76e9ccca6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-nexonia"></a><span data-ttu-id="9f353-103">Samouczek: Integracji Azure Active Directory z Nexonia</span><span class="sxs-lookup"><span data-stu-id="9f353-103">Tutorial: Azure Active Directory integration with Nexonia</span></span>

<span data-ttu-id="9f353-104">Z tego samouczka, dowiesz się, jak toointegrate Nexonia w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9f353-104">In this tutorial, you learn how toointegrate Nexonia with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9f353-105">Integracja z usługą Azure AD Nexonia zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="9f353-105">Integrating Nexonia with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9f353-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooNexonia</span><span class="sxs-lookup"><span data-stu-id="9f353-106">You can control in Azure AD who has access tooNexonia</span></span>
- <span data-ttu-id="9f353-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooNexonia (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f353-107">You can enable your users tooautomatically get signed-on tooNexonia (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9f353-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9f353-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9f353-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz.</span><span class="sxs-lookup"><span data-stu-id="9f353-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="9f353-110">[Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9f353-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f353-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9f353-111">Prerequisites</span></span>

<span data-ttu-id="9f353-112">tooconfigure integracji z usługą Azure AD z Nexonia należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9f353-112">tooconfigure Azure AD integration with Nexonia, you need hello following items:</span></span>

- <span data-ttu-id="9f353-113">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f353-113">An Azure AD subscription</span></span>
- <span data-ttu-id="9f353-114">Nexonia jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9f353-114">A Nexonia single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9f353-115">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="9f353-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9f353-116">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="9f353-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9f353-117">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9f353-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9f353-118">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9f353-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9f353-119">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="9f353-119">Scenario description</span></span>
<span data-ttu-id="9f353-120">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="9f353-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9f353-121">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="9f353-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9f353-122">Dodawanie Nexonia z galerii hello</span><span class="sxs-lookup"><span data-stu-id="9f353-122">Adding Nexonia from hello gallery</span></span>
2. <span data-ttu-id="9f353-123">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9f353-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-nexonia-from-hello-gallery"></a><span data-ttu-id="9f353-124">Dodawanie Nexonia z galerii hello</span><span class="sxs-lookup"><span data-stu-id="9f353-124">Adding Nexonia from hello gallery</span></span>
<span data-ttu-id="9f353-125">tooconfigure hello integracji Nexonia do usługi Azure AD, należy tooadd Nexonia z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="9f353-125">tooconfigure hello integration of Nexonia into Azure AD, you need tooadd Nexonia from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9f353-126">**tooadd Nexonia z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9f353-126">**tooadd Nexonia from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f353-127">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9f353-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="9f353-129">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="9f353-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9f353-130">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9f353-130">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="9f353-132">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9f353-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="9f353-134">W polu wyszukiwania hello wpisz **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="9f353-134">In hello search box, type **Nexonia**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_search.png)

5. <span data-ttu-id="9f353-136">W panelu wyników hello zaznacz **Nexonia**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="9f353-136">In hello results panel, select **Nexonia**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9f353-138">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9f353-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9f353-139">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Nexonia na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="9f353-139">In this section, you configure and test Azure AD single sign-on with Nexonia based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9f353-140">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Nexonia jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f353-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Nexonia is tooa user in Azure AD.</span></span> <span data-ttu-id="9f353-141">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Nexonia musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="9f353-141">In other words, a link relationship between an Azure AD user and hello related user in Nexonia needs toobe established.</span></span>

<span data-ttu-id="9f353-142">W Nexonia, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="9f353-142">In Nexonia, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9f353-143">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Nexonia, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="9f353-143">tooconfigure and test Azure AD single sign-on with Nexonia, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9f353-144">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="9f353-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9f353-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9f353-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9f353-146">**[Tworzenie użytkownika testowego Nexonia](#creating-a-nexonia-test-user)**  -toohave odpowiednikiem Simona Britta w Nexonia, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9f353-146">**[Creating a Nexonia test user](#creating-a-nexonia-test-user)** - toohave a counterpart of Britta Simon in Nexonia that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9f353-147">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9f353-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9f353-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="9f353-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9f353-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9f353-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9f353-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Nexonia.</span><span class="sxs-lookup"><span data-stu-id="9f353-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Nexonia application.</span></span>

>[!Note]
><span data-ttu-id="9f353-151">Jeśli występują problemy w hello integracji, zobacz to [łącze](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) dla przewodnik rozwiązywania problemów.</span><span class="sxs-lookup"><span data-stu-id="9f353-151">If you have issues in hello integration then refer this [link](https://docs.microsoft.com/azure/active-directory/application-sign-in-problem-federated-sso-gallery?WT.mc_id=UI_AAD_Enterprise_Apps_SupportOrTroubleshooting) for troubleshooting guide.</span></span> <span data-ttu-id="9f353-152">Jeśli nadal nie wykryto hello rozwiązania, następnie podnieść hello żądania obsługi z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9f353-152">If you still have not found hello solution, then raise hello support request from Azure portal.</span></span>

<span data-ttu-id="9f353-153">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Nexonia, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9f353-153">**tooconfigure Azure AD single sign-on with Nexonia, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f353-154">W portalu Azure na powitania hello **Nexonia** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="9f353-154">In hello Azure portal, on hello **Nexonia** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="9f353-156">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9f353-156">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_samlbase.png)

3. <span data-ttu-id="9f353-158">Na powitania **Nexonia domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9f353-158">On hello **Nexonia Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_url.png)

    <span data-ttu-id="9f353-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span><span class="sxs-lookup"><span data-stu-id="9f353-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://system.nexonia.com/assistant/saml.do?orgCode=<organizationcode>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9f353-161">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="9f353-161">This value is not real.</span></span> <span data-ttu-id="9f353-162">Zaktualizuj tę wartość przy hello rzeczywisty adres URL odpowiedzi służący.</span><span class="sxs-lookup"><span data-stu-id="9f353-162">Update this value with hello actual Reply URL.</span></span> <span data-ttu-id="9f353-163">Skontaktuj się z [zespołem pomocy technicznej Nexonia](https://nexonia.zendesk.com/hc/requests/new) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="9f353-163">Contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) tooget this value.</span></span> 


4. <span data-ttu-id="9f353-164">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="9f353-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_certificate.png) 

5. <span data-ttu-id="9f353-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9f353-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-nexonia-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9f353-168">Na powitania **konfiguracji Nexonia** kliknij **skonfigurować Nexonia** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="9f353-168">On hello **Nexonia Configuration** section, click **Configure Nexonia** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9f353-169">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="9f353-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_configure.png) 

7. <span data-ttu-id="9f353-171">tooget logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z [zespołem pomocy technicznej Nexonia](https://nexonia.zendesk.com/hc/requests/new) i podaj następujący hello:</span><span class="sxs-lookup"><span data-stu-id="9f353-171">tooget SSO configured for your application, contact [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) and provide them with hello following:</span></span>

    <span data-ttu-id="9f353-172">• hello pobrane **certyfikatu**</span><span class="sxs-lookup"><span data-stu-id="9f353-172">• hello downloaded **certificate**</span></span>

    <span data-ttu-id="9f353-173">• hello **identyfikator jednostki SAML**</span><span class="sxs-lookup"><span data-stu-id="9f353-173">• hello **SAML Entity ID**</span></span>

    <span data-ttu-id="9f353-174">• hello **SAML pojedynczy znak na adres URL usługi**</span><span class="sxs-lookup"><span data-stu-id="9f353-174">• hello **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="9f353-175">• hello **Sign-Out adresu URL**</span><span class="sxs-lookup"><span data-stu-id="9f353-175">• hello **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="9f353-176">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="9f353-176">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9f353-177">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="9f353-177">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9f353-178">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9f353-178">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9f353-179">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f353-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="9f353-180">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="9f353-180">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="9f353-182">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9f353-182">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f353-183">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9f353-183">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9f353-185">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="9f353-185">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9f353-187">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9f353-187">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9f353-189">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9f353-189">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-nexonia-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9f353-191">a.</span><span class="sxs-lookup"><span data-stu-id="9f353-191">a.</span></span> <span data-ttu-id="9f353-192">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9f353-192">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9f353-193">b.</span><span class="sxs-lookup"><span data-stu-id="9f353-193">b.</span></span> <span data-ttu-id="9f353-194">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9f353-194">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9f353-195">c.</span><span class="sxs-lookup"><span data-stu-id="9f353-195">c.</span></span> <span data-ttu-id="9f353-196">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="9f353-196">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9f353-197">d.</span><span class="sxs-lookup"><span data-stu-id="9f353-197">d.</span></span> <span data-ttu-id="9f353-198">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9f353-198">Click **Create**.</span></span>
 
### <a name="creating-a-nexonia-test-user"></a><span data-ttu-id="9f353-199">Tworzenie użytkownika testowego Nexonia</span><span class="sxs-lookup"><span data-stu-id="9f353-199">Creating a Nexonia test user</span></span>

<span data-ttu-id="9f353-200">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Nexonia.</span><span class="sxs-lookup"><span data-stu-id="9f353-200">In this section, you create a user called Britta Simon in Nexonia.</span></span> <span data-ttu-id="9f353-201">Praca z [zespołem pomocy technicznej Nexonia](https://nexonia.zendesk.com/hc/requests/new) tooadd hello użytkowników hello Nexonia platformy.</span><span class="sxs-lookup"><span data-stu-id="9f353-201">Work with [Nexonia support team](https://nexonia.zendesk.com/hc/requests/new) tooadd hello users in hello Nexonia platform.</span></span> <span data-ttu-id="9f353-202">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9f353-202">Users must be created and activated before you use single sign-on.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9f353-203">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f353-203">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9f353-204">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooNexonia.</span><span class="sxs-lookup"><span data-stu-id="9f353-204">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNexonia.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="9f353-206">**tooassign tooNexonia Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="9f353-206">**tooassign Britta Simon tooNexonia, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f353-207">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9f353-207">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="9f353-209">Z listy aplikacji hello wybierz **Nexonia**.</span><span class="sxs-lookup"><span data-stu-id="9f353-209">In hello applications list, select **Nexonia**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-nexonia-tutorial/tutorial_nexonia_app.png) 

3. <span data-ttu-id="9f353-211">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="9f353-211">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="9f353-213">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9f353-213">Click **Add** button.</span></span> <span data-ttu-id="9f353-214">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9f353-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="9f353-216">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9f353-216">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9f353-217">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9f353-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9f353-218">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9f353-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9f353-219">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9f353-219">Testing single sign-on</span></span>

<span data-ttu-id="9f353-220">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9f353-220">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9f353-221">Po kliknięciu kafelka Nexonia hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Nexonia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9f353-221">When you click hello Nexonia tile in hello Access Panel, you should get automatically signed-on tooyour Nexonia application.</span></span>
<span data-ttu-id="9f353-222">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="9f353-222">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9f353-223">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9f353-223">Additional resources</span></span>

* [<span data-ttu-id="9f353-224">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9f353-224">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9f353-225">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9f353-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-nexonia-tutorial/tutorial_general_203.png

