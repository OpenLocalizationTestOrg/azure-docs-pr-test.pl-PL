---
title: 'Samouczek: Integracji Azure Active Directory z Insperity ExpensAble | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Insperity ExpensAble."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c579c453-580e-417d-8a5e-9b6b352795c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: 204d5435c6ba1f23bb98701381e165a9a66add62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insperity-expensable"></a><span data-ttu-id="bb955-103">Samouczek: Integracji Azure Active Directory z Insperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="bb955-103">Tutorial: Azure Active Directory integration with Insperity ExpensAble</span></span>

<span data-ttu-id="bb955-104">Z tego samouczka, dowiesz się, jak toointegrate Insperity ExpensAble z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bb955-104">In this tutorial, you learn how toointegrate Insperity ExpensAble with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bb955-105">Integrowanie Insperity ExpensAble z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="bb955-105">Integrating Insperity ExpensAble with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bb955-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooInsperity ExpensAble</span><span class="sxs-lookup"><span data-stu-id="bb955-106">You can control in Azure AD who has access tooInsperity ExpensAble</span></span>
- <span data-ttu-id="bb955-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooInsperity ExpensAble (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb955-107">You can enable your users tooautomatically get signed-on tooInsperity ExpensAble (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bb955-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="bb955-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bb955-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bb955-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb955-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bb955-110">Prerequisites</span></span>

<span data-ttu-id="bb955-111">tooconfigure integracji z usługą Azure AD z Insperity ExpensAble należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="bb955-111">tooconfigure Azure AD integration with Insperity ExpensAble, you need hello following items:</span></span>

- <span data-ttu-id="bb955-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb955-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bb955-113">Insperity ExpensAble jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="bb955-113">An Insperity ExpensAble single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bb955-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="bb955-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bb955-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="bb955-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bb955-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="bb955-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bb955-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bb955-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bb955-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="bb955-118">Scenario description</span></span>
<span data-ttu-id="bb955-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="bb955-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bb955-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="bb955-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bb955-121">Dodawanie Insperity ExpensAble z galerii hello</span><span class="sxs-lookup"><span data-stu-id="bb955-121">Adding Insperity ExpensAble from hello gallery</span></span>
2. <span data-ttu-id="bb955-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bb955-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insperity-expensable-from-hello-gallery"></a><span data-ttu-id="bb955-123">Dodawanie Insperity ExpensAble z galerii hello</span><span class="sxs-lookup"><span data-stu-id="bb955-123">Adding Insperity ExpensAble from hello gallery</span></span>
<span data-ttu-id="bb955-124">tooconfigure hello integracji Insperity ExpensAble do usługi Azure AD, należy tooadd Insperity ExpensAble z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="bb955-124">tooconfigure hello integration of Insperity ExpensAble into Azure AD, you need tooadd Insperity ExpensAble from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bb955-125">**tooadd Insperity ExpensAble z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="bb955-125">**tooadd Insperity ExpensAble from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb955-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bb955-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="bb955-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="bb955-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bb955-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bb955-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="bb955-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bb955-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="bb955-133">W polu wyszukiwania hello wpisz **Insperity ExpensAble**.</span><span class="sxs-lookup"><span data-stu-id="bb955-133">In hello search box, type **Insperity ExpensAble**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_search.png)

5. <span data-ttu-id="bb955-135">W panelu wyników hello, wybierz **Insperity ExpensAble**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bb955-135">In hello results panel, select **Insperity ExpensAble**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bb955-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="bb955-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bb955-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Insperity ExpensAble w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="bb955-138">In this section, you configure and test Azure AD single sign-on with Insperity ExpensAble based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="bb955-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Insperity ExpensAble jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bb955-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Insperity ExpensAble is tooa user in Azure AD.</span></span> <span data-ttu-id="bb955-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Insperity ExpensAble musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="bb955-140">In other words, a link relationship between an Azure AD user and hello related user in Insperity ExpensAble needs toobe established.</span></span>

<span data-ttu-id="bb955-141">W Insperity ExpensAble przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="bb955-141">In Insperity ExpensAble, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bb955-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Insperity ExpensAble, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="bb955-142">tooconfigure and test Azure AD single sign-on with Insperity ExpensAble, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bb955-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="bb955-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bb955-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="bb955-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bb955-145">**[Tworzenie Insperity ExpensAble użytkownika testowego](#creating-an-insperity-expensable-test-user)**  -toohave odpowiednikiem Simona Britta w Insperity ExpensAble będący toohello połączonej usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bb955-145">**[Creating an Insperity ExpensAble test user](#creating-an-insperity-expensable-test-user)** - toohave a counterpart of Britta Simon in Insperity ExpensAble that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bb955-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bb955-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bb955-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="bb955-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bb955-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bb955-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bb955-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne Insperity ExpensAble aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bb955-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Insperity ExpensAble application.</span></span>

<span data-ttu-id="bb955-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Insperity ExpensAble wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="bb955-150">**tooconfigure Azure AD single sign-on with Insperity ExpensAble, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb955-151">W portalu Azure na powitania hello **Insperity ExpensAble** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="bb955-151">In hello Azure portal, on hello **Insperity ExpensAble** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="bb955-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="bb955-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_samlbase.png)

3. <span data-ttu-id="bb955-155">Na powitania **Insperity ExpensAble domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="bb955-155">On hello **Insperity ExpensAble Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_url.png)

    <span data-ttu-id="bb955-157">a.</span><span class="sxs-lookup"><span data-stu-id="bb955-157">a.</span></span> <span data-ttu-id="bb955-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span><span class="sxs-lookup"><span data-stu-id="bb955-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://server.expensable.com/esapp/Authenticate?companyId=<company ID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bb955-159">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="bb955-159">This value is not real.</span></span> <span data-ttu-id="bb955-160">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="bb955-160">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="bb955-161">Skontaktuj się z [zespołem pomocy technicznej klienta ExpensAble Insperity](http://expensable.com/support/support-overview) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="bb955-161">Contact [Insperity ExpensAble Client support team](http://expensable.com/support/support-overview) tooget this value.</span></span> 
 
4. <span data-ttu-id="bb955-162">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="bb955-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_certificate.png) 

5. <span data-ttu-id="bb955-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bb955-164">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bb955-166">Na powitania **konfiguracji ExpensAble Insperity** kliknij **skonfigurować ExpensAble Insperity** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="bb955-166">On hello **Insperity ExpensAble Configuration** section, click **Configure Insperity ExpensAble** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bb955-167">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="bb955-167">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_configure.png) 

7. <span data-ttu-id="bb955-169">tooconfigure rejestracji jednokrotnej w **Insperity ExpensAble** strony, należy pobrać hello toosend **XML metadanych**, **SAML pojedynczy znak na adres URL usługi** i **Identyfikator jednostki SAML** za[Insperity ExpensAble zespołem pomocy technicznej](http://expensable.com/support/support-overview).</span><span class="sxs-lookup"><span data-stu-id="bb955-169">tooconfigure single sign-on on **Insperity ExpensAble** side, you need toosend hello downloaded **Metadata XML**, **SAML Single Sign-On Service URL** and **SAML Entity ID** too[Insperity ExpensAble support team](http://expensable.com/support/support-overview).</span></span> <span data-ttu-id="bb955-170">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="bb955-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="bb955-171">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="bb955-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bb955-172">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="bb955-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bb955-173">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bb955-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bb955-174">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb955-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="bb955-175">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="bb955-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="bb955-177">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="bb955-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb955-178">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="bb955-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bb955-180">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="bb955-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bb955-182">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bb955-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bb955-184">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="bb955-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-insperityexpensable-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bb955-186">a.</span><span class="sxs-lookup"><span data-stu-id="bb955-186">a.</span></span> <span data-ttu-id="bb955-187">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bb955-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bb955-188">b.</span><span class="sxs-lookup"><span data-stu-id="bb955-188">b.</span></span> <span data-ttu-id="bb955-189">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bb955-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bb955-190">c.</span><span class="sxs-lookup"><span data-stu-id="bb955-190">c.</span></span> <span data-ttu-id="bb955-191">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="bb955-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bb955-192">d.</span><span class="sxs-lookup"><span data-stu-id="bb955-192">d.</span></span> <span data-ttu-id="bb955-193">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="bb955-193">Click **Create**.</span></span>
 
### <a name="creating-an-insperity-expensable-test-user"></a><span data-ttu-id="bb955-194">Tworzenie Insperity ExpensAble użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="bb955-194">Creating an Insperity ExpensAble test user</span></span>

<span data-ttu-id="bb955-195">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Insperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="bb955-195">hello objective of this section is toocreate a user called Britta Simon in Insperity ExpensAble.</span></span> <span data-ttu-id="bb955-196">We współpracy z [Insperity ExpensAble zespołem pomocy technicznej](http://expensable.com/support/support-overview) tooadd hello użytkowników w hello Insperity ExpensAble konta.</span><span class="sxs-lookup"><span data-stu-id="bb955-196">Please work with [Insperity ExpensAble support team](http://expensable.com/support/support-overview) tooadd hello users in hello Insperity ExpensAble account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bb955-197">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bb955-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bb955-198">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooInsperity ExpensAble.</span><span class="sxs-lookup"><span data-stu-id="bb955-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInsperity ExpensAble.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="bb955-200">**tooassign tooInsperity Simona Britta ExpensAble, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="bb955-200">**tooassign Britta Simon tooInsperity ExpensAble, perform hello following steps:**</span></span>

1. <span data-ttu-id="bb955-201">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="bb955-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="bb955-203">Z listy aplikacji hello wybierz **Insperity ExpensAble**.</span><span class="sxs-lookup"><span data-stu-id="bb955-203">In hello applications list, select **Insperity ExpensAble**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-insperityexpensable-tutorial/tutorial_insperityexpensable_app.png) 

3. <span data-ttu-id="bb955-205">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="bb955-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="bb955-207">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="bb955-207">Click **Add** button.</span></span> <span data-ttu-id="bb955-208">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bb955-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="bb955-210">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="bb955-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bb955-211">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bb955-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bb955-212">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="bb955-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bb955-213">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="bb955-213">Testing single sign-on</span></span>

<span data-ttu-id="bb955-214">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="bb955-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bb955-215">Po kliknięciu kafelka Insperity ExpensAble hello w hello Panel dostępu, należy pobrać zalogowane automatycznie tooyour Insperity ExpensAble aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bb955-215">When you click hello Insperity ExpensAble tile in hello Access Panel, you should get automatically signed-on tooyour Insperity ExpensAble application.</span></span>
<span data-ttu-id="bb955-216">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bb955-216">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="bb955-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="bb955-217">Additional resources</span></span>

* [<span data-ttu-id="bb955-218">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bb955-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bb955-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bb955-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insperityexpensable-tutorial/tutorial_general_203.png

