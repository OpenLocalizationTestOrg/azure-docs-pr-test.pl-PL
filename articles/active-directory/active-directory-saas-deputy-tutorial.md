---
title: "Samouczek: Integracji Azure Active Directory z zastępcy | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i zastępcy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 42f65b758682ce2513b6bb38ef40a19f955c88c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a><span data-ttu-id="5f40f-103">Samouczek: Integracji Azure Active Directory z zastępcy</span><span class="sxs-lookup"><span data-stu-id="5f40f-103">Tutorial: Azure Active Directory integration with Deputy</span></span>

<span data-ttu-id="5f40f-104">Z tego samouczka, dowiesz się, jak toointegrate zastępcy w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5f40f-104">In this tutorial, you learn how toointegrate Deputy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5f40f-105">Integracja z usługą Azure AD zastępcy zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5f40f-105">Integrating Deputy with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5f40f-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooDeputy</span><span class="sxs-lookup"><span data-stu-id="5f40f-106">You can control in Azure AD who has access tooDeputy</span></span>
- <span data-ttu-id="5f40f-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooDeputy (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f40f-107">You can enable your users tooautomatically get signed-on tooDeputy (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5f40f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5f40f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5f40f-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5f40f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f40f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5f40f-110">Prerequisites</span></span>

<span data-ttu-id="5f40f-111">tooconfigure integracji usługi Azure AD z zastępcy należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5f40f-111">tooconfigure Azure AD integration with Deputy, you need hello following items:</span></span>

- <span data-ttu-id="5f40f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f40f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5f40f-113">Zastępcy logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5f40f-113">A Deputy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5f40f-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5f40f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5f40f-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5f40f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5f40f-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5f40f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5f40f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5f40f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5f40f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5f40f-118">Scenario description</span></span>
<span data-ttu-id="5f40f-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5f40f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5f40f-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5f40f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5f40f-121">Dodawanie zastępcy z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5f40f-121">Adding Deputy from hello gallery</span></span>
2. <span data-ttu-id="5f40f-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5f40f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-deputy-from-hello-gallery"></a><span data-ttu-id="5f40f-123">Dodawanie zastępcy z galerii hello</span><span class="sxs-lookup"><span data-stu-id="5f40f-123">Adding Deputy from hello gallery</span></span>
<span data-ttu-id="5f40f-124">tooconfigure hello integracji zastępcy do usługi Azure AD, należy tooadd zastępcy z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5f40f-124">tooconfigure hello integration of Deputy into Azure AD, you need tooadd Deputy from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5f40f-125">**tooadd zastępcy z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5f40f-125">**tooadd Deputy from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f40f-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5f40f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="5f40f-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="5f40f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5f40f-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5f40f-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="5f40f-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5f40f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="5f40f-133">W polu wyszukiwania hello wpisz **zastępcy**.</span><span class="sxs-lookup"><span data-stu-id="5f40f-133">In hello search box, type **Deputy**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. <span data-ttu-id="5f40f-135">W panelu wyników hello zaznacz **zastępcy**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="5f40f-135">In hello results panel, select **Deputy**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5f40f-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5f40f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5f40f-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z zastępcy oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="5f40f-138">In this section, you configure and test Azure AD single sign-on with Deputy based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5f40f-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w zastępcy jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f40f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Deputy is tooa user in Azure AD.</span></span> <span data-ttu-id="5f40f-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w zastępcy musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="5f40f-140">In other words, a link relationship between an Azure AD user and hello related user in Deputy needs toobe established.</span></span>

<span data-ttu-id="5f40f-141">W zastępcy, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="5f40f-141">In Deputy, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5f40f-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z zastępcy, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="5f40f-142">tooconfigure and test Azure AD single sign-on with Deputy, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5f40f-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5f40f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5f40f-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5f40f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5f40f-145">**[Tworzenie użytkownika testowego zastępcy](#creating-a-deputy-test-user)**  -toohave odpowiednikiem Simona Britta w zastępcy, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="5f40f-145">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - toohave a counterpart of Britta Simon in Deputy that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5f40f-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5f40f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5f40f-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="5f40f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5f40f-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5f40f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5f40f-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji zastępcy.</span><span class="sxs-lookup"><span data-stu-id="5f40f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Deputy application.</span></span>

<span data-ttu-id="5f40f-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z zastępcy, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5f40f-150">**tooconfigure Azure AD single sign-on with Deputy, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f40f-151">W portalu Azure na powitania hello **zastępcy** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="5f40f-151">In hello Azure portal, on hello **Deputy** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="5f40f-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5f40f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. <span data-ttu-id="5f40f-155">Na powitania **zastępcy domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="5f40f-155">On hello **Deputy Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    <span data-ttu-id="5f40f-157">a.</span><span class="sxs-lookup"><span data-stu-id="5f40f-157">a.</span></span> <span data-ttu-id="5f40f-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="5f40f-158">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    <span data-ttu-id="5f40f-159">b.</span><span class="sxs-lookup"><span data-stu-id="5f40f-159">b.</span></span> <span data-ttu-id="5f40f-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="5f40f-160">In hello **Reply URL** textbox, type a URL using hello following pattern:</span></span>
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

4. <span data-ttu-id="5f40f-161">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="5f40f-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="5f40f-162">Jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="5f40f-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    <span data-ttu-id="5f40f-164">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<your-subdomain>.<region>.deputy.com`</span><span class="sxs-lookup"><span data-stu-id="5f40f-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<your-subdomain>.<region>.deputy.com`</span></span>
    
    >[!NOTE]
    > <span data-ttu-id="5f40f-165">Sufiks region zastępcy jest opcjonalne, lub go należy użyć jednej z tych: Australia | na | Europa | jako | la | af | | Australia Enterprise | Enterprise na | Enterprise eu | Enterprise — jako | Enterprise la | Enterprise af | usługi Enterprise</span><span class="sxs-lookup"><span data-stu-id="5f40f-165">Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5f40f-166">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="5f40f-166">These values are not real.</span></span> <span data-ttu-id="5f40f-167">Zaktualizować te wartości z hello rzeczywisty identyfikator, adres URL odpowiedzi i adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="5f40f-167">Update these values with hello actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="5f40f-168">Skontaktuj się z [zespołem pomocy technicznej zastępcy](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="5f40f-168">Contact [Deputy support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) tooget these values.</span></span> 

5. <span data-ttu-id="5f40f-169">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="5f40f-169">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. <span data-ttu-id="5f40f-171">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5f40f-171">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="5f40f-173">Na powitania **konfiguracji zastępcy** kliknij **skonfigurować zastępcy** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="5f40f-173">On hello **Deputy Configuration** section, click **Configure Deputy** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5f40f-174">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="5f40f-174">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. <span data-ttu-id="5f40f-176">Przejdź toohello następującego adresu URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span><span class="sxs-lookup"><span data-stu-id="5f40f-176">Navigate toohello following URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span></span> <span data-ttu-id="5f40f-177">Przejdź za**ustawienia zabezpieczeń** i kliknij przycisk **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="5f40f-177">Go too**Security Settings** and click **Edit**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. <span data-ttu-id="5f40f-179">Na tym **ustawienia zabezpieczeń** wykonaj następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="5f40f-179">On this **Security Settings** page, perform below steps.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    <span data-ttu-id="5f40f-181">a.</span><span class="sxs-lookup"><span data-stu-id="5f40f-181">a.</span></span> <span data-ttu-id="5f40f-182">Włącz **społecznościowych logowania**.</span><span class="sxs-lookup"><span data-stu-id="5f40f-182">Enable **Social Login**.</span></span>
   
    <span data-ttu-id="5f40f-183">b.</span><span class="sxs-lookup"><span data-stu-id="5f40f-183">b.</span></span> <span data-ttu-id="5f40f-184">Otwórz z certyfikatu szyfrowania Base64 pobrany z portalu Azure w programie Notatnik hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu biblioteki OpenSSL** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5f40f-184">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **OpenSSL Certificate** textbox.</span></span>
   
    <span data-ttu-id="5f40f-185">c.</span><span class="sxs-lookup"><span data-stu-id="5f40f-185">c.</span></span> <span data-ttu-id="5f40f-186">W polu tekstowym adres URL logowania jednokrotnego SAML hello wpisz`https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span><span class="sxs-lookup"><span data-stu-id="5f40f-186">In hello SAML SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span></span>
    
    <span data-ttu-id="5f40f-187">d.</span><span class="sxs-lookup"><span data-stu-id="5f40f-187">d.</span></span> <span data-ttu-id="5f40f-188">W polu tekstowym adres URL logowania jednokrotnego SAML hello, Zastąp `<your subdomain>` z Twojej domeny podrzędnej.</span><span class="sxs-lookup"><span data-stu-id="5f40f-188">In hello SAML SSO URL textbox, replace `<your subdomain>` with your subdomain.</span></span>
   
    <span data-ttu-id="5f40f-189">e.</span><span class="sxs-lookup"><span data-stu-id="5f40f-189">e.</span></span> <span data-ttu-id="5f40f-190">W polu tekstowym adres URL logowania jednokrotnego SAML hello, Zastąp `<saml sso url>` z hello **SAML pojedynczy znak na adres URL usługi** zostały skopiowane z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5f40f-190">In hello SAML SSO URL textbox, replace `<saml sso url>` with hello **SAML Single Sign-On Service URL** you have copied from hello Azure portal.</span></span>
   
    <span data-ttu-id="5f40f-191">f.</span><span class="sxs-lookup"><span data-stu-id="5f40f-191">f.</span></span> <span data-ttu-id="5f40f-192">Kliknij przycisk **Zapisz ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="5f40f-192">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="5f40f-193">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="5f40f-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5f40f-194">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="5f40f-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5f40f-195">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5f40f-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5f40f-196">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f40f-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="5f40f-197">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="5f40f-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="5f40f-199">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="5f40f-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f40f-200">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="5f40f-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5f40f-202">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="5f40f-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5f40f-204">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5f40f-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5f40f-206">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5f40f-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5f40f-208">a.</span><span class="sxs-lookup"><span data-stu-id="5f40f-208">a.</span></span> <span data-ttu-id="5f40f-209">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5f40f-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5f40f-210">b.</span><span class="sxs-lookup"><span data-stu-id="5f40f-210">b.</span></span> <span data-ttu-id="5f40f-211">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5f40f-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5f40f-212">c.</span><span class="sxs-lookup"><span data-stu-id="5f40f-212">c.</span></span> <span data-ttu-id="5f40f-213">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="5f40f-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5f40f-214">d.</span><span class="sxs-lookup"><span data-stu-id="5f40f-214">d.</span></span> <span data-ttu-id="5f40f-215">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5f40f-215">Click **Create**.</span></span>
 
### <a name="creating-a-deputy-test-user"></a><span data-ttu-id="5f40f-216">Tworzenie użytkownika testowego zastępcy</span><span class="sxs-lookup"><span data-stu-id="5f40f-216">Creating a Deputy test user</span></span>

<span data-ttu-id="5f40f-217">toolog użytkowników tooenable usługi Azure AD w tooDeputy, muszą mieć przydzielone do zastępcy.</span><span class="sxs-lookup"><span data-stu-id="5f40f-217">tooenable Azure AD users toolog in tooDeputy, they must be provisioned into Deputy.</span></span> <span data-ttu-id="5f40f-218">W przypadku zastępcy Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="5f40f-218">In case of Deputy, provisioning is a manual task.</span></span>

#### <a name="tooprovision-a-user-account-perform-hello-following-steps"></a><span data-ttu-id="5f40f-219">tooprovision konta użytkownika, należy wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="5f40f-219">tooprovision a user account, perform hello following steps:</span></span>
1. <span data-ttu-id="5f40f-220">Zaloguj się w witrynie firmy zastępcy tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="5f40f-220">Log in tooyour Deputy company site as an administrator.</span></span>

2. <span data-ttu-id="5f40f-221">W okienku nawigacji w górnym powitania kliknij **osób**.</span><span class="sxs-lookup"><span data-stu-id="5f40f-221">On hello top navigation pane, click **People**.</span></span>
   
   <span data-ttu-id="5f40f-222">![Osoby](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "osób")</span><span class="sxs-lookup"><span data-stu-id="5f40f-222">![People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "People")</span></span>

3. <span data-ttu-id="5f40f-223">Kliknij przycisk hello **dodawania osoby** przycisk **dodać jedną osobę**.</span><span class="sxs-lookup"><span data-stu-id="5f40f-223">Click hello **Add People** button and click **Add a single person**.</span></span>
   
   <span data-ttu-id="5f40f-224">![Dodaj użytkowników](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Dodaj użytkowników")</span><span class="sxs-lookup"><span data-stu-id="5f40f-224">![Add People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Add People")</span></span>

4. <span data-ttu-id="5f40f-225">Wykonaj następujące kroki hello, a następnie kliknij przycisk **Zapisz & zaprosić**.</span><span class="sxs-lookup"><span data-stu-id="5f40f-225">Perform hello following steps and click **Save & Invite**.</span></span>
   
   <span data-ttu-id="5f40f-226">![Nowy użytkownik](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="5f40f-226">![New User](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "New User")</span></span>

   <span data-ttu-id="5f40f-227">a.</span><span class="sxs-lookup"><span data-stu-id="5f40f-227">a.</span></span> <span data-ttu-id="5f40f-228">W hello **nazwa** pole tekstowe, nazwa typu hello użytkownika, takich jak **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5f40f-228">In hello **Name** textbox, type name of hello user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="5f40f-229">b.</span><span class="sxs-lookup"><span data-stu-id="5f40f-229">b.</span></span> <span data-ttu-id="5f40f-230">W hello **E-mail** pole tekstowe, typ hello adres e-mail konta usługi Azure AD ma tooprovision.</span><span class="sxs-lookup"><span data-stu-id="5f40f-230">In hello **Email** textbox, type hello email address of an Azure AD account you want tooprovision.</span></span>
   
   <span data-ttu-id="5f40f-231">c.</span><span class="sxs-lookup"><span data-stu-id="5f40f-231">c.</span></span> <span data-ttu-id="5f40f-232">W hello **działania na** pole tekstowe, nazwa firmy hello typu.</span><span class="sxs-lookup"><span data-stu-id="5f40f-232">In hello **Work at** textbox, type hello business name.</span></span>
   
   <span data-ttu-id="5f40f-233">d.</span><span class="sxs-lookup"><span data-stu-id="5f40f-233">d.</span></span> <span data-ttu-id="5f40f-234">Kliknij przycisk **Zapisz & zaprosić** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5f40f-234">Click **Save & Invite** button.</span></span>

5. <span data-ttu-id="5f40f-235">Właściciel konta usługi AAD Hello otrzymuje wiadomość e-mail i następuje tooconfirm łącze swojego konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="5f40f-235">hello AAD account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span> <span data-ttu-id="5f40f-236">Możesz użyć innych zastępcy użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez tooprovision zastępcy AAD kont użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5f40f-236">You can use any other Deputy user account creation tools or APIs provided by Deputy tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5f40f-237">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f40f-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5f40f-238">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooDeputy.</span><span class="sxs-lookup"><span data-stu-id="5f40f-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDeputy.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="5f40f-240">**tooassign tooDeputy Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="5f40f-240">**tooassign Britta Simon tooDeputy, perform hello following steps:**</span></span>

1. <span data-ttu-id="5f40f-241">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="5f40f-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5f40f-243">Z listy aplikacji hello wybierz **zastępcy**.</span><span class="sxs-lookup"><span data-stu-id="5f40f-243">In hello applications list, select **Deputy**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. <span data-ttu-id="5f40f-245">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="5f40f-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="5f40f-247">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5f40f-247">Click **Add** button.</span></span> <span data-ttu-id="5f40f-248">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5f40f-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="5f40f-250">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5f40f-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5f40f-251">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5f40f-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5f40f-252">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5f40f-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5f40f-253">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5f40f-253">Testing single sign-on</span></span>

<span data-ttu-id="5f40f-254">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5f40f-254">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="5f40f-255">Po kliknięciu hello zastępcy kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour zastępcy aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5f40f-255">When you click hello Deputy tile in hello Access Panel, you should get automatically signed-on tooyour Deputy application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5f40f-256">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5f40f-256">Additional resources</span></span>

* [<span data-ttu-id="5f40f-257">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5f40f-257">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5f40f-258">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5f40f-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_203.png

