---
title: 'Samouczek: Integracji Azure Active Directory z Aravo | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Aravo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 224939d8-2c9c-4561-968d-62722f5ab5ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 8f1336fa307fa9e8d625440a573d9f9d79dd820b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aravo"></a><span data-ttu-id="9d31a-103">Samouczek: Integracji Azure Active Directory z Aravo</span><span class="sxs-lookup"><span data-stu-id="9d31a-103">Tutorial: Azure Active Directory integration with Aravo</span></span>

<span data-ttu-id="9d31a-104">Z tego samouczka, dowiesz się, jak toointegrate Aravo w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9d31a-104">In this tutorial, you learn how toointegrate Aravo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9d31a-105">Integracja z usługą Azure AD Aravo zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="9d31a-105">Integrating Aravo with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9d31a-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooAravo</span><span class="sxs-lookup"><span data-stu-id="9d31a-106">You can control in Azure AD who has access tooAravo</span></span>
- <span data-ttu-id="9d31a-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAravo (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d31a-107">You can enable your users tooautomatically get signed-on tooAravo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9d31a-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9d31a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9d31a-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9d31a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d31a-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9d31a-110">Prerequisites</span></span>

<span data-ttu-id="9d31a-111">tooconfigure integracji z usługą Azure AD z Aravo należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9d31a-111">tooconfigure Azure AD integration with Aravo, you need hello following items:</span></span>

- <span data-ttu-id="9d31a-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d31a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9d31a-113">Aravo jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9d31a-113">An Aravo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9d31a-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="9d31a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9d31a-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="9d31a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9d31a-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9d31a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9d31a-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9d31a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9d31a-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="9d31a-118">Scenario description</span></span>
<span data-ttu-id="9d31a-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="9d31a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9d31a-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="9d31a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9d31a-121">Dodawanie Aravo z galerii hello</span><span class="sxs-lookup"><span data-stu-id="9d31a-121">Adding Aravo from hello gallery</span></span>
2. <span data-ttu-id="9d31a-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9d31a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aravo-from-hello-gallery"></a><span data-ttu-id="9d31a-123">Dodawanie Aravo z galerii hello</span><span class="sxs-lookup"><span data-stu-id="9d31a-123">Adding Aravo from hello gallery</span></span>
<span data-ttu-id="9d31a-124">tooconfigure hello integracji Aravo do usługi Azure AD, należy tooadd Aravo z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="9d31a-124">tooconfigure hello integration of Aravo into Azure AD, you need tooadd Aravo from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9d31a-125">**tooadd Aravo z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9d31a-125">**tooadd Aravo from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d31a-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9d31a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="9d31a-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="9d31a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9d31a-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9d31a-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="9d31a-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9d31a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="9d31a-133">W polu wyszukiwania hello wpisz **Aravo**.</span><span class="sxs-lookup"><span data-stu-id="9d31a-133">In hello search box, type **Aravo**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_search.png)

5. <span data-ttu-id="9d31a-135">W panelu wyników hello zaznacz **Aravo**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="9d31a-135">In hello results panel, select **Aravo**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9d31a-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9d31a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9d31a-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Aravo na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="9d31a-138">In this section, you configure and test Azure AD single sign-on with Aravo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9d31a-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Aravo jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d31a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Aravo is tooa user in Azure AD.</span></span> <span data-ttu-id="9d31a-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Aravo musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="9d31a-140">In other words, a link relationship between an Azure AD user and hello related user in Aravo needs toobe established.</span></span>

<span data-ttu-id="9d31a-141">W Aravo, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="9d31a-141">In Aravo, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9d31a-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Aravo, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="9d31a-142">tooconfigure and test Azure AD single sign-on with Aravo, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9d31a-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="9d31a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9d31a-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9d31a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9d31a-145">**[Tworzenie użytkownika testowego Aravo](#creating-an-aravo-test-user)**  -toohave odpowiednikiem Simona Britta w Aravo, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9d31a-145">**[Creating an Aravo test user](#creating-an-aravo-test-user)** - toohave a counterpart of Britta Simon in Aravo that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9d31a-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9d31a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9d31a-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="9d31a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9d31a-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9d31a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9d31a-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Aravo.</span><span class="sxs-lookup"><span data-stu-id="9d31a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Aravo application.</span></span>

<span data-ttu-id="9d31a-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Aravo, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9d31a-150">**tooconfigure Azure AD single sign-on with Aravo, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d31a-151">W portalu Azure na powitania hello **Aravo** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="9d31a-151">In hello Azure portal, on hello **Aravo** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="9d31a-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9d31a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_samlbase.png)

3. <span data-ttu-id="9d31a-155">Na powitania **Aravo domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9d31a-155">On hello **Aravo Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_url.png)

    <span data-ttu-id="9d31a-157">a.</span><span class="sxs-lookup"><span data-stu-id="9d31a-157">a.</span></span> <span data-ttu-id="9d31a-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.aravo.com`</span><span class="sxs-lookup"><span data-stu-id="9d31a-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.aravo.com`</span></span>

    <span data-ttu-id="9d31a-159">b.</span><span class="sxs-lookup"><span data-stu-id="9d31a-159">b.</span></span> <span data-ttu-id="9d31a-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.aravo.com/aems/login.do`</span><span class="sxs-lookup"><span data-stu-id="9d31a-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<companyname>.aravo.com/aems/login.do`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9d31a-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="9d31a-161">These values are not real.</span></span> <span data-ttu-id="9d31a-162">Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="9d31a-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="9d31a-163">Skontaktuj się z [zespołem pomocy technicznej Aravo](http://www.aravo.com/about-us/contact/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="9d31a-163">Contact [Aravo support team](http://www.aravo.com/about-us/contact/) tooget these values.</span></span>
 
4. <span data-ttu-id="9d31a-164">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="9d31a-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_certificate.png) 

5. <span data-ttu-id="9d31a-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9d31a-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-aravo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9d31a-168">Na powitania **konfiguracji Aravo** kliknij **skonfigurować Aravo** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="9d31a-168">On hello **Aravo Configuration** section, click **Configure Aravo** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9d31a-169">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="9d31a-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_configure.png) 

7. <span data-ttu-id="9d31a-171">tooconfigure rejestracji jednokrotnej w **Aravo** strony, należy pobrać hello toosend **certyfikatu (Base64)**, **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi**za[zespołem pomocy technicznej Aravo](http://www.aravo.com/about-us/contact/).</span><span class="sxs-lookup"><span data-stu-id="9d31a-171">tooconfigure single sign-on on **Aravo** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Aravo support team](http://www.aravo.com/about-us/contact/).</span></span> 


> [!TIP]
> <span data-ttu-id="9d31a-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="9d31a-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9d31a-173">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="9d31a-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9d31a-174">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9d31a-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9d31a-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d31a-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="9d31a-176">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="9d31a-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="9d31a-178">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9d31a-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d31a-179">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9d31a-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9d31a-181">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="9d31a-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9d31a-183">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9d31a-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9d31a-185">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9d31a-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9d31a-187">a.</span><span class="sxs-lookup"><span data-stu-id="9d31a-187">a.</span></span> <span data-ttu-id="9d31a-188">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9d31a-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9d31a-189">b.</span><span class="sxs-lookup"><span data-stu-id="9d31a-189">b.</span></span> <span data-ttu-id="9d31a-190">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9d31a-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9d31a-191">c.</span><span class="sxs-lookup"><span data-stu-id="9d31a-191">c.</span></span> <span data-ttu-id="9d31a-192">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="9d31a-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9d31a-193">d.</span><span class="sxs-lookup"><span data-stu-id="9d31a-193">d.</span></span> <span data-ttu-id="9d31a-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9d31a-194">Click **Create**.</span></span>
 
### <a name="creating-an-aravo-test-user"></a><span data-ttu-id="9d31a-195">Tworzenie użytkownika testowego Aravo</span><span class="sxs-lookup"><span data-stu-id="9d31a-195">Creating an Aravo test user</span></span>

<span data-ttu-id="9d31a-196">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Aravo.</span><span class="sxs-lookup"><span data-stu-id="9d31a-196">hello objective of this section is toocreate a user called Britta Simon in Aravo.</span></span> <span data-ttu-id="9d31a-197">Praca z [zespołem pomocy technicznej Aravo](http://www.aravo.com/about-us/contact/) tooadd hello użytkowników w hello Aravo konta.</span><span class="sxs-lookup"><span data-stu-id="9d31a-197">Work with [Aravo support team](http://www.aravo.com/about-us/contact/) tooadd hello users in hello Aravo account.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9d31a-198">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9d31a-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9d31a-199">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAravo.</span><span class="sxs-lookup"><span data-stu-id="9d31a-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAravo.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="9d31a-201">**tooassign tooAravo Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="9d31a-201">**tooassign Britta Simon tooAravo, perform hello following steps:**</span></span>

1. <span data-ttu-id="9d31a-202">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9d31a-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="9d31a-204">Z listy aplikacji hello wybierz **Aravo**.</span><span class="sxs-lookup"><span data-stu-id="9d31a-204">In hello applications list, select **Aravo**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_app.png) 

3. <span data-ttu-id="9d31a-206">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="9d31a-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="9d31a-208">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9d31a-208">Click **Add** button.</span></span> <span data-ttu-id="9d31a-209">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9d31a-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="9d31a-211">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9d31a-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9d31a-212">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9d31a-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9d31a-213">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9d31a-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9d31a-214">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9d31a-214">Testing single sign-on</span></span>

<span data-ttu-id="9d31a-215">Celem Hello w tej sekcji jest tootest z usługi Microsoft Azure AD rejestracji jednokrotnej konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9d31a-215">hello objective of this section is tootest your Microsoft Azure AD Single Sign-On configuration using hello Access Panel.</span></span>

<span data-ttu-id="9d31a-216">Po kliknięciu kafelka Aravo hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Aravo aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9d31a-216">When you click hello Aravo tile in hello Access Panel, you should get automatically signed-on tooyour Aravo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9d31a-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9d31a-217">Additional resources</span></span>

* [<span data-ttu-id="9d31a-218">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9d31a-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9d31a-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9d31a-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_203.png

