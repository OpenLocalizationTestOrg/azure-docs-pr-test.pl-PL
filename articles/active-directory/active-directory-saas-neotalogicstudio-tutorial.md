---
title: 'Samouczek: Integracji Azure Active Directory z Neota logiki Studio | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Neota logiki Studio."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 842605e6-a91d-42cc-a0bb-e23e67173ae2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: jeedes
ms.openlocfilehash: a479ee49618de8275132dbc2c21a8ef723d92d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-neota-logic-studio"></a><span data-ttu-id="5e037-103">Samouczek: Integracji Azure Active Directory z Neota logiki Studio</span><span class="sxs-lookup"><span data-stu-id="5e037-103">Tutorial: Azure Active Directory integration with Neota Logic Studio</span></span>

<span data-ttu-id="5e037-104">Z tego samouczka, dowiesz się, jak toointegrate Neota logiki Studio w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5e037-104">In this tutorial, you learn how toointegrate Neota Logic Studio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5e037-105">Integracja z usługą Azure AD Neota logiki Studio udostępnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5e037-105">Integrating Neota Logic Studio with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5e037-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooNeota w Studio logiki</span><span class="sxs-lookup"><span data-stu-id="5e037-106">You can control in Azure AD who has access tooNeota Logic Studio</span></span>
- <span data-ttu-id="5e037-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooNeota Studio logiki (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e037-107">You can enable your users tooautomatically get signed-on tooNeota Logic Studio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5e037-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5e037-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5e037-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz.</span><span class="sxs-lookup"><span data-stu-id="5e037-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="5e037-110">[Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5e037-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e037-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5e037-111">Prerequisites</span></span>

<span data-ttu-id="5e037-112">tooconfigure integracji usługi Azure AD z Studio logiki Neota należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5e037-112">tooconfigure Azure AD integration with Neota Logic Studio, you need hello following items:</span></span>

- <span data-ttu-id="5e037-113">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e037-113">An Azure AD subscription</span></span>
- <span data-ttu-id="5e037-114">Neota logiki Studio jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5e037-114">A Neota Logic Studio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5e037-115">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5e037-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5e037-116">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5e037-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5e037-117">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5e037-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5e037-118">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5e037-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5e037-119">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5e037-119">Scenario description</span></span>

<span data-ttu-id="5e037-120">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5e037-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5e037-121">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5e037-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5e037-122">Dodawanie Studio logiki Neota z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5e037-122">Adding Neota Logic Studio from hello gallery</span></span>
2. <span data-ttu-id="5e037-123">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5e037-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-neota-logic-studio-from-hello-gallery"></a><span data-ttu-id="5e037-124">Dodawanie Studio logiki Neota z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5e037-124">Adding Neota Logic Studio from hello gallery</span></span>

<span data-ttu-id="5e037-125">tooconfigure hello integracji Neota Studio logiki w usłudze Azure Active Directory, należy tooadd Studio logiki Neota z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5e037-125">tooconfigure hello integration of Neota Logic Studio into Azure AD, you need tooadd Neota Logic Studio from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5e037-126">**tooadd Neota Studio logiki z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5e037-126">**tooadd Neota Logic Studio from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e037-127">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5e037-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="5e037-129">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5e037-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5e037-130">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5e037-130">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="5e037-132">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5e037-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="5e037-134">W polu wyszukiwania hello wpisz **Studio logiki Neota**.</span><span class="sxs-lookup"><span data-stu-id="5e037-134">In hello search box, type **Neota Logic Studio**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_search.png)

5. <span data-ttu-id="5e037-136">W panelu wyników hello, wybierz **Studio logiki Neota**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5e037-136">In hello results panel, select **Neota Logic Studio**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5e037-138">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5e037-138">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="5e037-139">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Studio logiki Neota oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="5e037-139">In this section, you configure and test Azure AD single sign-on with Neota Logic Studio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5e037-140">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Studio logiki Neota jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5e037-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Neota Logic Studio is tooa user in Azure AD.</span></span> <span data-ttu-id="5e037-141">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Studio logiki Neota musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="5e037-141">In other words, a link relationship between an Azure AD user and hello related user in Neota Logic Studio needs toobe established.</span></span>

<span data-ttu-id="5e037-142">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Studio logiki Neota.</span><span class="sxs-lookup"><span data-stu-id="5e037-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Neota Logic Studio.</span></span>

<span data-ttu-id="5e037-143">tooconfigure i test usługi Azure AD rejestracji jednokrotnej z Studio logiki Neota należy hello toocomplete po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="5e037-143">tooconfigure and test Azure AD single sign-on with Neota Logic Studio, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5e037-144">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5e037-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5e037-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5e037-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5e037-146">**[Tworzenie użytkownika testowego Studio logiki Neota](#creating-a-neota-logic-studio-test-user)**  -toohave odpowiednikiem Simona Britta w Studio logiki Neota, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5e037-146">**[Creating a Neota Logic Studio test user](#creating-a-neota-logic-studio-test-user)** - toohave a counterpart of Britta Simon in Neota Logic Studio that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5e037-147">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5e037-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5e037-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="5e037-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5e037-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5e037-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5e037-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne Neota Studio logiki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5e037-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Neota Logic Studio application.</span></span>

<span data-ttu-id="5e037-151">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Studio logiki Neota, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5e037-151">**tooconfigure Azure AD single sign-on with Neota Logic Studio, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e037-152">W portalu Azure na powitania hello **Studio logiki Neota** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5e037-152">In hello Azure portal, on hello **Neota Logic Studio** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="5e037-154">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5e037-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_samlbase.png)

3. <span data-ttu-id="5e037-156">Na powitania **Neota logiki Studio domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="5e037-156">On hello **Neota Logic Studio Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_url.png)

    <span data-ttu-id="5e037-158">a.</span><span class="sxs-lookup"><span data-stu-id="5e037-158">a.</span></span> <span data-ttu-id="5e037-159">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<sub domain>.neotalogic.com/a/<sub application>`</span><span class="sxs-lookup"><span data-stu-id="5e037-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<sub domain>.neotalogic.com/a/<sub application>`</span></span>

    <span data-ttu-id="5e037-160">b.</span><span class="sxs-lookup"><span data-stu-id="5e037-160">b.</span></span> <span data-ttu-id="5e037-161">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<sub domain>.neotalogic.com/wb`</span><span class="sxs-lookup"><span data-stu-id="5e037-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<sub domain>.neotalogic.com/wb`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5e037-162">Wartości te nie są hello prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="5e037-162">These values are not hello real.</span></span> <span data-ttu-id="5e037-163">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="5e037-163">Update these values with hello actual Sign-On URL & Identifier.</span></span> <span data-ttu-id="5e037-164">W tym miejscu zalecamy możesz toouse hello unikatową wartość ciągu w hello identyfikator.</span><span class="sxs-lookup"><span data-stu-id="5e037-164">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="5e037-165">Skontaktuj się z [zespołem pomocy technicznej klienta Studio logiki Neota](https://www.neotalogic.com/contact-us/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="5e037-165">Contact [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="5e037-166">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5e037-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_certificate.png) 

5. <span data-ttu-id="5e037-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5e037-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5e037-170">tooget skonfigurowany dla aplikacji, skontaktuj się z logowania jednokrotnego [Obsługa Studio logiki Neota](https://www.neotalogic.com/contact-us/) zespołu i zapewnić ich z pobrane **XML metadanych** pliku.</span><span class="sxs-lookup"><span data-stu-id="5e037-170">tooget SSO configured for your application, Contact [Neota Logic Studio support](https://www.neotalogic.com/contact-us/) team and provide them with downloaded **Metadata XML** file.</span></span>

> [!TIP]
> <span data-ttu-id="5e037-171">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="5e037-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5e037-172">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="5e037-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5e037-173">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5e037-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5e037-174">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e037-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="5e037-175">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="5e037-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="5e037-177">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5e037-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e037-178">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5e037-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5e037-180">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5e037-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5e037-182">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5e037-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5e037-184">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5e037-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5e037-186">a.</span><span class="sxs-lookup"><span data-stu-id="5e037-186">a.</span></span> <span data-ttu-id="5e037-187">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5e037-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5e037-188">b.</span><span class="sxs-lookup"><span data-stu-id="5e037-188">b.</span></span> <span data-ttu-id="5e037-189">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5e037-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5e037-190">c.</span><span class="sxs-lookup"><span data-stu-id="5e037-190">c.</span></span> <span data-ttu-id="5e037-191">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="5e037-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5e037-192">d.</span><span class="sxs-lookup"><span data-stu-id="5e037-192">d.</span></span> <span data-ttu-id="5e037-193">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5e037-193">Click **Create**.</span></span>
 
### <a name="creating-a-neota-logic-studio-test-user"></a><span data-ttu-id="5e037-194">Tworzenie użytkownika testowego Neota logiki Studio</span><span class="sxs-lookup"><span data-stu-id="5e037-194">Creating a Neota Logic Studio test user</span></span>

<span data-ttu-id="5e037-195">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Studio logiki Neota.</span><span class="sxs-lookup"><span data-stu-id="5e037-195">In this section, you create a user called Britta Simon in Neota Logic Studio.</span></span> <span data-ttu-id="5e037-196">Korzystanie z [zespołem pomocy technicznej klienta Studio logiki Neota](https://www.neotalogic.com/contact-us/) do dodawania użytkowników hello hello Studio logiki Neota platformy.</span><span class="sxs-lookup"><span data-stu-id="5e037-196">work with [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to add hello users in hello Neota Logic Studio platform.</span></span> <span data-ttu-id="5e037-197">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5e037-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5e037-198">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5e037-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5e037-199">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooNeota w Studio logiki.</span><span class="sxs-lookup"><span data-stu-id="5e037-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNeota Logic Studio.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="5e037-201">**tooassign Simona Britta tooNeota w Studio logiki wykonywania hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5e037-201">**tooassign Britta Simon tooNeota Logic Studio, perform hello following steps:**</span></span>

1. <span data-ttu-id="5e037-202">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5e037-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5e037-204">Z listy aplikacji hello wybierz **Studio logiki Neota**.</span><span class="sxs-lookup"><span data-stu-id="5e037-204">In hello applications list, select **Neota Logic Studio**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_app.png) 

3. <span data-ttu-id="5e037-206">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5e037-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="5e037-208">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5e037-208">Click **Add** button.</span></span> <span data-ttu-id="5e037-209">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5e037-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="5e037-211">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5e037-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5e037-212">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5e037-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5e037-213">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5e037-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5e037-214">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5e037-214">Testing single sign-on</span></span>

<span data-ttu-id="5e037-215">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5e037-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5e037-216">Kliknij Kafelek Studio logiki Neota hello w hello panelu dostępu będzie przekierowanego tooOrganization Zaloguj się na stronie.</span><span class="sxs-lookup"><span data-stu-id="5e037-216">Click hello Neota Logic Studio tile in hello Access Panel, you will be redirected tooOrganization sign-on page.</span></span> <span data-ttu-id="5e037-217">Po pomyślnym logowaniu będzie zalogowane tooyour Neota Studio logiki aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5e037-217">After successful login, you will be signed-on tooyour Neota Logic Studio application.</span></span> <span data-ttu-id="5e037-218">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="5e037-218">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

<span data-ttu-id="5e037-219">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="5e037-219">For more information about hello Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="5e037-220">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5e037-220">Additional resources</span></span>

* [<span data-ttu-id="5e037-221">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5e037-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5e037-222">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5e037-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_203.png

