---
title: 'Samouczek: Integracji Azure Active Directory z Oneteam | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Oneteam."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2e94916c-64ae-4e1a-a8b5-bc6ef7d28c29
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 7964aaaf9b9570d460f28d86de34b5e87693ba93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oneteam"></a><span data-ttu-id="8576e-103">Samouczek: Integracji Azure Active Directory z Oneteam</span><span class="sxs-lookup"><span data-stu-id="8576e-103">Tutorial: Azure Active Directory integration with Oneteam</span></span>

<span data-ttu-id="8576e-104">Z tego samouczka, dowiesz się, jak toointegrate Oneteam w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8576e-104">In this tutorial, you learn how toointegrate Oneteam with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8576e-105">Integracja z usługą Azure AD Oneteam zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8576e-105">Integrating Oneteam with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8576e-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooOneteam</span><span class="sxs-lookup"><span data-stu-id="8576e-106">You can control in Azure AD who has access tooOneteam</span></span>
- <span data-ttu-id="8576e-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooOneteam (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8576e-107">You can enable your users tooautomatically get signed-on tooOneteam (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8576e-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8576e-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8576e-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8576e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8576e-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8576e-110">Prerequisites</span></span>

<span data-ttu-id="8576e-111">tooconfigure integracji z usługą Azure AD z Oneteam należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8576e-111">tooconfigure Azure AD integration with Oneteam, you need hello following items:</span></span>

- <span data-ttu-id="8576e-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8576e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8576e-113">Oneteam logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8576e-113">A Oneteam single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8576e-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8576e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8576e-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8576e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8576e-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8576e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8576e-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8576e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8576e-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8576e-118">Scenario description</span></span>
<span data-ttu-id="8576e-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8576e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8576e-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8576e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8576e-121">Dodawanie Oneteam z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8576e-121">Adding Oneteam from hello gallery</span></span>
2. <span data-ttu-id="8576e-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8576e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oneteam-from-hello-gallery"></a><span data-ttu-id="8576e-123">Dodawanie Oneteam z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8576e-123">Adding Oneteam from hello gallery</span></span>
<span data-ttu-id="8576e-124">tooconfigure hello integracji Oneteam do usługi Azure AD, należy tooadd Oneteam z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8576e-124">tooconfigure hello integration of Oneteam into Azure AD, you need tooadd Oneteam from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8576e-125">**tooadd Oneteam z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8576e-125">**tooadd Oneteam from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8576e-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8576e-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="8576e-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8576e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8576e-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8576e-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="8576e-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8576e-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="8576e-133">W polu wyszukiwania hello wpisz **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="8576e-133">In hello search box, type **Oneteam**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_search.png)

5. <span data-ttu-id="8576e-135">W panelu wyników hello zaznacz **Oneteam**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8576e-135">In hello results panel, select **Oneteam**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8576e-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8576e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8576e-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Oneteam w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="8576e-138">In this section, you configure and test Azure AD single sign-on with Oneteam based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8576e-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Oneteam jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8576e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Oneteam is tooa user in Azure AD.</span></span> <span data-ttu-id="8576e-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Oneteam musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="8576e-140">In other words, a link relationship between an Azure AD user and hello related user in Oneteam needs toobe established.</span></span>

<span data-ttu-id="8576e-141">W Oneteam, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="8576e-141">In Oneteam, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8576e-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Oneteam, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8576e-142">tooconfigure and test Azure AD single sign-on with Oneteam, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8576e-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="8576e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8576e-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8576e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8576e-145">**[Tworzenie użytkownika testowego Oneteam](#creating-a-oneteam-test-user)**  -toohave odpowiednikiem Simona Britta w Oneteam, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8576e-145">**[Creating a Oneteam test user](#creating-a-oneteam-test-user)** - toohave a counterpart of Britta Simon in Oneteam that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8576e-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8576e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8576e-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="8576e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8576e-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8576e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8576e-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Oneteam.</span><span class="sxs-lookup"><span data-stu-id="8576e-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Oneteam application.</span></span>

<span data-ttu-id="8576e-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Oneteam, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8576e-150">**tooconfigure Azure AD single sign-on with Oneteam, perform hello following steps:**</span></span>

1. <span data-ttu-id="8576e-151">W portalu Azure na powitania hello **Oneteam** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="8576e-151">In hello Azure portal, on hello **Oneteam** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="8576e-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8576e-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_samlbase.png)

3. <span data-ttu-id="8576e-155">Na powitania **Oneteam domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="8576e-155">On hello **Oneteam Domain and URLs** section, if you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_url.png)

    <span data-ttu-id="8576e-157">a.</span><span class="sxs-lookup"><span data-stu-id="8576e-157">a.</span></span> <span data-ttu-id="8576e-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://api.one-team.io/teams/<team name>`</span><span class="sxs-lookup"><span data-stu-id="8576e-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://api.one-team.io/teams/<team name>`</span></span>

    <span data-ttu-id="8576e-159">b.</span><span class="sxs-lookup"><span data-stu-id="8576e-159">b.</span></span> <span data-ttu-id="8576e-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://api.one-team.io/teams/<team name>/auth/saml/callback`</span><span class="sxs-lookup"><span data-stu-id="8576e-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://api.one-team.io/teams/<team name>/auth/saml/callback`</span></span>

4. <span data-ttu-id="8576e-161">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="8576e-161">Check **Show advanced URL settings**, if you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_url1.png)

    <span data-ttu-id="8576e-163">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<team name>.one-team.io/`</span><span class="sxs-lookup"><span data-stu-id="8576e-163">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<team name>.one-team.io/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="8576e-164">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="8576e-164">These values are not real.</span></span> <span data-ttu-id="8576e-165">Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="8576e-165">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="8576e-166">Skontaktuj się z [zespołem pomocy technicznej klienta Oneteam](https://support.one-team.com/hc/requests/new) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="8576e-166">Contact [Oneteam Client support team](https://support.one-team.com/hc/requests/new) tooget these values.</span></span> 



5. <span data-ttu-id="8576e-167">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="8576e-167">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_certificate.png) 

6. <span data-ttu-id="8576e-169">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8576e-169">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-oneteam-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="8576e-171">tooget logowania jednokrotnego skonfigurowane dla aplikacji, można zwiększyć hello biletu pomocy technicznej z [zespołem pomocy technicznej Oneteam](https://support.one-team.com/hc/requests/new) i podaj hello pobrane **metadanych**.</span><span class="sxs-lookup"><span data-stu-id="8576e-171">tooget SSO configured for your application, you can raise hello support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new) and provide them hello downloaded **Metadata**.</span></span> 

> [!TIP]
> <span data-ttu-id="8576e-172">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="8576e-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8576e-173">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="8576e-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8576e-174">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8576e-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8576e-175">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8576e-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="8576e-176">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="8576e-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="8576e-178">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8576e-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8576e-179">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8576e-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8576e-181">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="8576e-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8576e-183">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8576e-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8576e-185">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8576e-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8576e-187">a.</span><span class="sxs-lookup"><span data-stu-id="8576e-187">a.</span></span> <span data-ttu-id="8576e-188">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8576e-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8576e-189">b.</span><span class="sxs-lookup"><span data-stu-id="8576e-189">b.</span></span> <span data-ttu-id="8576e-190">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8576e-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8576e-191">c.</span><span class="sxs-lookup"><span data-stu-id="8576e-191">c.</span></span> <span data-ttu-id="8576e-192">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="8576e-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8576e-193">d.</span><span class="sxs-lookup"><span data-stu-id="8576e-193">d.</span></span> <span data-ttu-id="8576e-194">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8576e-194">Click **Create**.</span></span>
 
### <a name="creating-a-oneteam-test-user"></a><span data-ttu-id="8576e-195">Tworzenie użytkownika testowego Oneteam</span><span class="sxs-lookup"><span data-stu-id="8576e-195">Creating a Oneteam test user</span></span>

<span data-ttu-id="8576e-196">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Oneteam.</span><span class="sxs-lookup"><span data-stu-id="8576e-196">hello objective of this section is toocreate a user called Britta Simon in Oneteam.</span></span> <span data-ttu-id="8576e-197">Oneteam obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="8576e-197">Oneteam supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="8576e-198">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="8576e-198">There is no action item for you in this section.</span></span> <span data-ttu-id="8576e-199">Nowy użytkownik zostanie utworzony podczas próby tooaccess Oneteam, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="8576e-199">A new user will be created during an attempt tooaccess Oneteam, if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="8576e-200">Jeśli potrzebujesz toocreate użytkownika ręcznie, może wiązać się hello biletu pomocy technicznej z [zespołem pomocy technicznej Oneteam](https://support.one-team.com/hc/requests/new).</span><span class="sxs-lookup"><span data-stu-id="8576e-200">If you need toocreate an user manually, you can raise hello support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8576e-201">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8576e-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8576e-202">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooOneteam.</span><span class="sxs-lookup"><span data-stu-id="8576e-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOneteam.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="8576e-204">**tooassign tooOneteam Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="8576e-204">**tooassign Britta Simon tooOneteam, perform hello following steps:**</span></span>

1. <span data-ttu-id="8576e-205">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8576e-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8576e-207">Z listy aplikacji hello wybierz **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="8576e-207">In hello applications list, select **Oneteam**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_app.png) 

3. <span data-ttu-id="8576e-209">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8576e-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="8576e-211">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8576e-211">Click **Add** button.</span></span> <span data-ttu-id="8576e-212">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8576e-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="8576e-214">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8576e-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8576e-215">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8576e-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8576e-216">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8576e-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8576e-217">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8576e-217">Testing single sign-on</span></span>

<span data-ttu-id="8576e-218">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8576e-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8576e-219">Po kliknięciu kafelka Oneteam hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Oneteam aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8576e-219">When you click hello Oneteam tile in hello Access Panel, you should get automatically signed-on tooyour Oneteam application.</span></span>
<span data-ttu-id="8576e-220">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8576e-220">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8576e-221">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8576e-221">Additional resources</span></span>

* [<span data-ttu-id="8576e-222">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8576e-222">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8576e-223">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8576e-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_203.png

