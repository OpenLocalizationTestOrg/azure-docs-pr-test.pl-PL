---
title: 'Samouczek: Integracji Azure Active Directory z MaxxPoint | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i MaxxPoint."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ba026e-96fc-4ae8-b135-0169da810e99
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 03b13908add8d8c62f1d1480ed2288658fce14d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-maxxpoint"></a><span data-ttu-id="d4672-103">Samouczek: Integracji Azure Active Directory z MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="d4672-103">Tutorial: Azure Active Directory integration with MaxxPoint</span></span>

<span data-ttu-id="d4672-104">Z tego samouczka, dowiesz się, jak toointegrate MaxxPoint w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d4672-104">In this tutorial, you learn how toointegrate MaxxPoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d4672-105">Integracja z usługą Azure AD MaxxPoint zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d4672-105">Integrating MaxxPoint with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d4672-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooMaxxPoint</span><span class="sxs-lookup"><span data-stu-id="d4672-106">You can control in Azure AD who has access tooMaxxPoint</span></span>
- <span data-ttu-id="d4672-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooMaxxPoint (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4672-107">You can enable your users tooautomatically get signed-on tooMaxxPoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d4672-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d4672-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d4672-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d4672-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d4672-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d4672-110">Prerequisites</span></span>

<span data-ttu-id="d4672-111">tooconfigure integracji z usługą Azure AD z MaxxPoint należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d4672-111">tooconfigure Azure AD integration with MaxxPoint, you need hello following items:</span></span>

- <span data-ttu-id="d4672-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4672-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d4672-113">MaxxPoint jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d4672-113">A MaxxPoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d4672-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d4672-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d4672-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d4672-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d4672-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d4672-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d4672-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d4672-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d4672-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d4672-118">Scenario description</span></span>
<span data-ttu-id="d4672-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d4672-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d4672-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d4672-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d4672-121">Dodawanie MaxxPoint z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d4672-121">Adding MaxxPoint from hello gallery</span></span>
2. <span data-ttu-id="d4672-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d4672-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-maxxpoint-from-hello-gallery"></a><span data-ttu-id="d4672-123">Dodawanie MaxxPoint z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d4672-123">Adding MaxxPoint from hello gallery</span></span>
<span data-ttu-id="d4672-124">tooconfigure hello integracji MaxxPoint do usługi Azure AD, należy tooadd MaxxPoint z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d4672-124">tooconfigure hello integration of MaxxPoint into Azure AD, you need tooadd MaxxPoint from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d4672-125">**tooadd MaxxPoint z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d4672-125">**tooadd MaxxPoint from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d4672-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d4672-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="d4672-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d4672-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d4672-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d4672-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="d4672-131">Kliknij przycisk **nowej aplikacji** przycisk na powitania górnej części okna dialogowego tooadd nowej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d4672-131">Click **New application** button on hello top of dialog tooadd new application.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="d4672-133">W polu wyszukiwania hello wpisz **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="d4672-133">In hello search box, type **MaxxPoint**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_001.png)

5. <span data-ttu-id="d4672-135">W panelu wyników hello zaznacz **MaxxPoint**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d4672-135">In hello results panel, select **MaxxPoint**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_0001.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d4672-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d4672-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d4672-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z MaxxPoint w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="d4672-138">In this section, you configure and test Azure AD single sign-on with MaxxPoint based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d4672-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w MaxxPoint jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d4672-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in MaxxPoint is tooa user in Azure AD.</span></span> <span data-ttu-id="d4672-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w MaxxPoint musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="d4672-140">In other words, a link relationship between an Azure AD user and hello related user in MaxxPoint needs toobe established.</span></span>

<span data-ttu-id="d4672-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d4672-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in MaxxPoint.</span></span>

<span data-ttu-id="d4672-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z MaxxPoint, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d4672-142">tooconfigure and test Azure AD single sign-on with MaxxPoint, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d4672-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d4672-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d4672-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d4672-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d4672-145">**[Tworzenie użytkownika testowego MaxxPoint](#creating-a-maxxpoint-test-user)**  -toohave odpowiednikiem Simona Britta w MaxxPoint, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d4672-145">**[Creating a MaxxPoint test user](#creating-a-maxxpoint-test-user)** - toohave a counterpart of Britta Simon in MaxxPoint that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="d4672-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d4672-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d4672-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="d4672-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d4672-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d4672-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d4672-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d4672-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your MaxxPoint application.</span></span>

<span data-ttu-id="d4672-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z MaxxPoint, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d4672-150">**tooconfigure Azure AD single sign-on with MaxxPoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="d4672-151">W portalu Azure na powitania hello **MaxxPoint** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d4672-151">In hello Azure portal, on hello **MaxxPoint** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="d4672-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d4672-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_300.png)

3. <span data-ttu-id="d4672-155">Na powitania **MaxxPoint domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP zainicjował tryb**, nie należy tooperform żadnych czynności.</span><span class="sxs-lookup"><span data-stu-id="d4672-155">On hello **MaxxPoint Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, no need tooperform any steps.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_02.png)
    
4. <span data-ttu-id="d4672-157">Na powitania **MaxxPoint domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **SP zainicjował tryb**, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d4672-157">On hello **MaxxPoint Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_03.png)

    <span data-ttu-id="d4672-159">a.</span><span class="sxs-lookup"><span data-stu-id="d4672-159">a.</span></span> <span data-ttu-id="d4672-160">Kliknij przycisk **Pokaż zaawansowane ustawienia adresu URL** opcji</span><span class="sxs-lookup"><span data-stu-id="d4672-160">Click **Show advanced URL settings** option</span></span>

    <span data-ttu-id="d4672-161">b.</span><span class="sxs-lookup"><span data-stu-id="d4672-161">b.</span></span> <span data-ttu-id="d4672-162">W hello **na adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span><span class="sxs-lookup"><span data-stu-id="d4672-162">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://maxxpoint.westipc.com/default/sso/login/entity/<customer-id>-azure`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d4672-163">Należy pamiętać, że nie jest hello rzeczywistą wartość.</span><span class="sxs-lookup"><span data-stu-id="d4672-163">Please note that this is not hello real value.</span></span> <span data-ttu-id="d4672-164">Masz tooupdate tej wartości z rzeczywistego hello Zaloguj się na adres URL.</span><span class="sxs-lookup"><span data-stu-id="d4672-164">You have tooupdate this value with hello actual Sign On URL.</span></span> <span data-ttu-id="d4672-165">Wywołanie MaxxPoint zespołu na **888-728-0950** tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="d4672-165">Call MaxxPoint team on **888-728-0950** tooget this value.</span></span>

5. <span data-ttu-id="d4672-166">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d4672-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_06.png) 

6. <span data-ttu-id="d4672-168">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d4672-168">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="d4672-170">tooget logowania jednokrotnego skonfigurować aplikację tak, aby wywołać MaxxPoint zespołem pomocy technicznej dla **888-728-0950** i będzie można dodatkowo assist na sposób pobierania ich hello tooprovide **XML metadanych** pliku.</span><span class="sxs-lookup"><span data-stu-id="d4672-170">tooget SSO configured for your application, call MaxxPoint support team on **888-728-0950** and they'll assist you further on how tooprovide them hello downloaded **Metadata XML** file.</span></span> 

> [!TIP]
> <span data-ttu-id="d4672-171">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="d4672-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d4672-172">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="d4672-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d4672-173">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d4672-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d4672-174">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4672-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="d4672-175">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="d4672-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="d4672-177">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d4672-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d4672-178">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d4672-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d4672-180">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d4672-180">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d4672-182">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d4672-182">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d4672-184">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d4672-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-maxxpoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d4672-186">a.</span><span class="sxs-lookup"><span data-stu-id="d4672-186">a.</span></span> <span data-ttu-id="d4672-187">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d4672-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d4672-188">b.</span><span class="sxs-lookup"><span data-stu-id="d4672-188">b.</span></span> <span data-ttu-id="d4672-189">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d4672-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d4672-190">c.</span><span class="sxs-lookup"><span data-stu-id="d4672-190">c.</span></span> <span data-ttu-id="d4672-191">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="d4672-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d4672-192">d.</span><span class="sxs-lookup"><span data-stu-id="d4672-192">d.</span></span> <span data-ttu-id="d4672-193">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d4672-193">Click **Create**.</span></span> 

### <a name="creating-a-maxxpoint-test-user"></a><span data-ttu-id="d4672-194">Tworzenie użytkownika testowego MaxxPoint</span><span class="sxs-lookup"><span data-stu-id="d4672-194">Creating a MaxxPoint test user</span></span>

<span data-ttu-id="d4672-195">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w MaxxPoint.</span><span class="sxs-lookup"><span data-stu-id="d4672-195">In this section, you create a user called Britta Simon in MaxxPoint.</span></span> <span data-ttu-id="d4672-196">Skontaktuj się z działem MaxxPoint zespołem pomocy technicznej na **888-728-0950** tooadd hello użytkowników w hello MaxxPoint aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d4672-196">Please call MaxxPoint support team on **888-728-0950** tooadd hello users in hello MaxxPoint application.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d4672-197">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d4672-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d4672-198">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooMaxxPoint dostępu.</span><span class="sxs-lookup"><span data-stu-id="d4672-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooMaxxPoint.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="d4672-200">**tooassign tooMaxxPoint Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d4672-200">**tooassign Britta Simon tooMaxxPoint, perform hello following steps:**</span></span>

1. <span data-ttu-id="d4672-201">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d4672-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d4672-203">Z listy aplikacji hello wybierz **MaxxPoint**.</span><span class="sxs-lookup"><span data-stu-id="d4672-203">In hello applications list, select **MaxxPoint**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-maxxpoint-tutorial/tutorial_maxxpoint_50.png) 

3. <span data-ttu-id="d4672-205">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d4672-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="d4672-207">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d4672-207">Click **Add** button.</span></span> <span data-ttu-id="d4672-208">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d4672-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="d4672-210">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d4672-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d4672-211">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d4672-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d4672-212">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d4672-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d4672-213">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d4672-213">Testing single sign-on</span></span>

<span data-ttu-id="d4672-214">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d4672-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d4672-215">Po kliknięciu kafelka MaxxPoint hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour MaxxPoint aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d4672-215">When you click hello MaxxPoint tile in hello Access Panel, you should get automatically signed-on tooyour MaxxPoint application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d4672-216">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d4672-216">Additional resources</span></span>

* [<span data-ttu-id="d4672-217">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d4672-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d4672-218">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d4672-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-maxxpoint-tutorial/tutorial_general_203.png