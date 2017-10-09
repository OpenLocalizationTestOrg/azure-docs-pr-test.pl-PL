---
title: 'Samouczek: Integracji Azure Active Directory z ITRP | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i ITRP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e09716a3-4200-4853-9414-2390e6c10d98
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 35463a55fcfc1e55c90700737961c1ff2e58992a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-itrp"></a><span data-ttu-id="ac574-103">Samouczek: Integracji Azure Active Directory z ITRP</span><span class="sxs-lookup"><span data-stu-id="ac574-103">Tutorial: Azure Active Directory integration with ITRP</span></span>

<span data-ttu-id="ac574-104">Z tego samouczka, dowiesz się, jak toointegrate ITRP w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ac574-104">In this tutorial, you learn how toointegrate ITRP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ac574-105">Integracja z usługą Azure AD ITRP zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ac574-105">Integrating ITRP with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ac574-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooITRP</span><span class="sxs-lookup"><span data-stu-id="ac574-106">You can control in Azure AD who has access tooITRP</span></span>
- <span data-ttu-id="ac574-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooITRP (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac574-107">You can enable your users tooautomatically get signed-on tooITRP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ac574-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="ac574-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ac574-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ac574-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac574-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ac574-110">Prerequisites</span></span>

<span data-ttu-id="ac574-111">tooconfigure integracji z usługą Azure AD z ITRP należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ac574-111">tooconfigure Azure AD integration with ITRP, you need hello following items:</span></span>

- <span data-ttu-id="ac574-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac574-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ac574-113">ITRP logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="ac574-113">An ITRP single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ac574-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ac574-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ac574-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ac574-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ac574-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ac574-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ac574-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ac574-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ac574-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ac574-118">Scenario description</span></span>
<span data-ttu-id="ac574-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ac574-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ac574-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ac574-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ac574-121">Dodawanie ITRP z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ac574-121">Adding ITRP from hello gallery</span></span>
2. <span data-ttu-id="ac574-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ac574-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-itrp-from-hello-gallery"></a><span data-ttu-id="ac574-123">Dodawanie ITRP z galerii hello</span><span class="sxs-lookup"><span data-stu-id="ac574-123">Adding ITRP from hello gallery</span></span>
<span data-ttu-id="ac574-124">tooconfigure hello integracji ITRP w tooAzure AD, należy tooadd ITRP z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ac574-124">tooconfigure hello integration of ITRP in tooAzure AD, you need tooadd ITRP from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ac574-125">**tooadd ITRP z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ac574-125">**tooadd ITRP from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac574-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ac574-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ac574-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ac574-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ac574-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ac574-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ac574-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ac574-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ac574-133">W polu wyszukiwania hello wpisz **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="ac574-133">In hello search box, type **ITRP**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_search.png)

5. <span data-ttu-id="ac574-135">W panelu wyników hello zaznacz **ITRP**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ac574-135">In hello results panel, select **ITRP**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ac574-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="ac574-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="ac574-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ITRP na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="ac574-138">In this section, you configure and test Azure AD single sign-on with ITRP based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ac574-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w ITRP jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac574-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ITRP is tooa user in Azure AD.</span></span> <span data-ttu-id="ac574-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w ITRP musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="ac574-140">In other words, a link relationship between an Azure AD user and hello related user in ITRP needs toobe established.</span></span>

<span data-ttu-id="ac574-141">W ITRP, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="ac574-141">In ITRP, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="ac574-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z ITRP, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="ac574-142">tooconfigure and test Azure AD single sign-on with ITRP, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ac574-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ac574-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ac574-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ac574-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ac574-145">**[Użytkownik testowy tworzenie ITRP](#creating-an-itrp-test-user)**  -toohave odpowiednikiem Simona Britta w ITRP, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ac574-145">**[Creating an ITRP test user](#creating-an-itrp-test-user)** - toohave a counterpart of Britta Simon in ITRP that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ac574-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ac574-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ac574-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="ac574-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ac574-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ac574-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ac574-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji ITRP.</span><span class="sxs-lookup"><span data-stu-id="ac574-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ITRP application.</span></span>

<span data-ttu-id="ac574-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z ITRP, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ac574-150">**tooconfigure Azure AD single sign-on with ITRP, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac574-151">W portalu Azure na powitania hello **ITRP** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ac574-151">In hello Azure portal, on hello **ITRP** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ac574-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ac574-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_samlbase.png)

3. <span data-ttu-id="ac574-155">Na powitania **ITRP domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ac574-155">On hello **ITRP Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_url.png)

    <span data-ttu-id="ac574-157">a.</span><span class="sxs-lookup"><span data-stu-id="ac574-157">a.</span></span> <span data-ttu-id="ac574-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="ac574-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.itrp.com`</span></span>

    <span data-ttu-id="ac574-159">b.</span><span class="sxs-lookup"><span data-stu-id="ac574-159">b.</span></span> <span data-ttu-id="ac574-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenant-name>.itrp.com`</span><span class="sxs-lookup"><span data-stu-id="ac574-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<tenant-name>.itrp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ac574-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="ac574-161">These values are not real.</span></span> <span data-ttu-id="ac574-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="ac574-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="ac574-163">Skontaktuj się z [zespołem pomocy technicznej klienta ITRP](https://www.itrp.com/support) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="ac574-163">Contact [ITRP Client support team](https://www.itrp.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="ac574-164">Na powitania **certyfikat podpisywania SAML** hello kopiowania, sekcji **odcisk PALCA** wartości certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="ac574-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_certificate.png) 

5. <span data-ttu-id="ac574-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ac574-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-itrp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ac574-168">Na powitania **konfiguracji ITRP** kliknij **skonfigurować ITRP** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="ac574-168">On hello **ITRP Configuration** section, click **Configure ITRP** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="ac574-169">Kopiuj hello **SAML pojedynczy znak na adres URL usługi i adres URL Sign-Out** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="ac574-169">Copy hello **SAML Single Sign-On Service URL and Sign-Out URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_configure.png) 

7. <span data-ttu-id="ac574-171">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy ITRP tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="ac574-171">In a different web browser window, log in tooyour ITRP company site as an administrator.</span></span>

8. <span data-ttu-id="ac574-172">Witaj pasku narzędzi u góry hello, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="ac574-172">In hello toolbar on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="ac574-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span><span class="sxs-lookup"><span data-stu-id="ac574-173">![ITRP](./media/active-directory-saas-itrp-tutorial/ic775570.png "ITRP")</span></span>

8. <span data-ttu-id="ac574-174">Wybierz w okienku nawigacji po lewej stronie powitania **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="ac574-174">In hello left navigation pane, select **Single Sign-On**.</span></span>
   
    <span data-ttu-id="ac574-175">![Logowanie jednokrotne](./media/active-directory-saas-itrp-tutorial/ic775571.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="ac574-175">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775571.png "Single Sign-On")</span></span>

9. <span data-ttu-id="ac574-176">W hello rejestracji jednokrotnej sekcji konfiguracji wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ac574-176">In hello Single Sign-On configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="ac574-177">![Logowanie jednokrotne](./media/active-directory-saas-itrp-tutorial/ic775572.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="ac574-177">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775572.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="ac574-178">![Logowanie jednokrotne](./media/active-directory-saas-itrp-tutorial/ic775573.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="ac574-178">![Single Sign-On](./media/active-directory-saas-itrp-tutorial/ic775573.png "Single Sign-On")</span></span>   

    <span data-ttu-id="ac574-179">a.</span><span class="sxs-lookup"><span data-stu-id="ac574-179">a.</span></span> <span data-ttu-id="ac574-180">Kliknij przycisk **Włącz**.</span><span class="sxs-lookup"><span data-stu-id="ac574-180">Click **Enable**.</span></span>

    <span data-ttu-id="ac574-181">b.</span><span class="sxs-lookup"><span data-stu-id="ac574-181">b.</span></span> <span data-ttu-id="ac574-182">W **zdalnego adresu URL wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out URL**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ac574-182">In **Remote Log Out URL** textbox, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ac574-183">c.</span><span class="sxs-lookup"><span data-stu-id="ac574-183">c.</span></span> <span data-ttu-id="ac574-184">W **adres URL logowania jednokrotnego SAML** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ac574-184">In **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ac574-185">d.In **odcisk palca certyfikatu** pole tekstowe, Wklej hello **odcisk palca** wartość certyfikatów, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ac574-185">d.In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span> 
      
10. <span data-ttu-id="ac574-186">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ac574-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="ac574-187">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="ac574-187">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="ac574-188">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="ac574-188">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="ac574-189">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="ac574-189">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ac574-190">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac574-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="ac574-191">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="ac574-191">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ac574-193">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ac574-193">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac574-194">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ac574-194">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ac574-196">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ac574-196">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ac574-198">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ac574-198">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ac574-200">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ac574-200">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-itrp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ac574-202">a.</span><span class="sxs-lookup"><span data-stu-id="ac574-202">a.</span></span> <span data-ttu-id="ac574-203">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ac574-203">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ac574-204">b.</span><span class="sxs-lookup"><span data-stu-id="ac574-204">b.</span></span> <span data-ttu-id="ac574-205">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ac574-205">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ac574-206">c.</span><span class="sxs-lookup"><span data-stu-id="ac574-206">c.</span></span> <span data-ttu-id="ac574-207">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="ac574-207">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ac574-208">d.</span><span class="sxs-lookup"><span data-stu-id="ac574-208">d.</span></span> <span data-ttu-id="ac574-209">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ac574-209">Click **Create**.</span></span>
 
### <a name="creating-an-itrp-test-user"></a><span data-ttu-id="ac574-210">Tworzenie użytkownika testowego ITRP</span><span class="sxs-lookup"><span data-stu-id="ac574-210">Creating an ITRP test user</span></span>

<span data-ttu-id="ac574-211">toolog użytkowników tooenable usługi Azure AD w tooITRP, muszą mieć przydzielone w tooITRP.</span><span class="sxs-lookup"><span data-stu-id="ac574-211">tooenable Azure AD users toolog in tooITRP, they must be provisioned in tooITRP.</span></span>  

<span data-ttu-id="ac574-212">W przypadku hello ITRP Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="ac574-212">In hello case of ITRP, provisioning is a manual task.</span></span>

<span data-ttu-id="ac574-213">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ac574-213">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac574-214">Zaloguj się za tooyour **ITRP** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="ac574-214">Log in tooyour **ITRP** tenant.</span></span>

2. <span data-ttu-id="ac574-215">Witaj pasku narzędzi u góry hello, kliknij przycisk **rekordów**.</span><span class="sxs-lookup"><span data-stu-id="ac574-215">In hello toolbar on hello top, click **Records**.</span></span>
   
    <span data-ttu-id="ac574-216">![Administrator](./media/active-directory-saas-itrp-tutorial/ic775575.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="ac574-216">![Admin](./media/active-directory-saas-itrp-tutorial/ic775575.png "Admin")</span></span>

3. <span data-ttu-id="ac574-217">Wybierz z menu podręcznego hello **osób**.</span><span class="sxs-lookup"><span data-stu-id="ac574-217">From hello popup menu, select **People**.</span></span>
   
    <span data-ttu-id="ac574-218">![Osoby](./media/active-directory-saas-itrp-tutorial/ic775587.png "osób")</span><span class="sxs-lookup"><span data-stu-id="ac574-218">![People](./media/active-directory-saas-itrp-tutorial/ic775587.png "People")</span></span>

4. <span data-ttu-id="ac574-219">Kliknij przycisk **Dodawanie nowej osoby** ("+").</span><span class="sxs-lookup"><span data-stu-id="ac574-219">Click **Add New Person** (“+”).</span></span>
   
    <span data-ttu-id="ac574-220">![Administrator](./media/active-directory-saas-itrp-tutorial/ic775576.png "administratora")</span><span class="sxs-lookup"><span data-stu-id="ac574-220">![Admin](./media/active-directory-saas-itrp-tutorial/ic775576.png "Admin")</span></span>

5. <span data-ttu-id="ac574-221">W oknie dialogowym Dodawanie nowej osoby hello wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ac574-221">On hello Add New Person dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="ac574-222">![Użytkownik](./media/active-directory-saas-itrp-tutorial/ic775577.png "użytkownika")</span><span class="sxs-lookup"><span data-stu-id="ac574-222">![User](./media/active-directory-saas-itrp-tutorial/ic775577.png "User")</span></span> 
      
    <span data-ttu-id="ac574-223">a.</span><span class="sxs-lookup"><span data-stu-id="ac574-223">a.</span></span> <span data-ttu-id="ac574-224">Typ hello **nazwa**, **poczty E-mail** ma tooprovision poprawnego konta usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="ac574-224">Type hello **Name**, **Email** of a valid AAD account you want tooprovision.</span></span>

    <span data-ttu-id="ac574-225">b.</span><span class="sxs-lookup"><span data-stu-id="ac574-225">b.</span></span> <span data-ttu-id="ac574-226">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ac574-226">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="ac574-227">Możesz użyć innych ITRP użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez ITRP tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="ac574-227">You can use any other ITRP user account creation tools or APIs provided by ITRP tooprovision AAD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ac574-228">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ac574-228">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ac574-229">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooITRP.</span><span class="sxs-lookup"><span data-stu-id="ac574-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooITRP.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ac574-231">**tooassign tooITRP Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ac574-231">**tooassign Britta Simon tooITRP, perform hello following steps:**</span></span>

1. <span data-ttu-id="ac574-232">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ac574-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ac574-234">Z listy aplikacji hello wybierz **ITRP**.</span><span class="sxs-lookup"><span data-stu-id="ac574-234">In hello applications list, select **ITRP**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-itrp-tutorial/tutorial_itrp_app.png) 

3. <span data-ttu-id="ac574-236">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ac574-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ac574-238">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ac574-238">Click **Add** button.</span></span> <span data-ttu-id="ac574-239">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ac574-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ac574-241">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="ac574-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ac574-242">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ac574-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ac574-243">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ac574-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ac574-244">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ac574-244">Testing single sign-on</span></span>

<span data-ttu-id="ac574-245">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ac574-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="ac574-246">Po kliknięciu hello ITRP kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour ITRP aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ac574-246">When you click hello ITRP tile in hello Access Panel, you should get automatically signed-on tooyour ITRP application.</span></span>
<span data-ttu-id="ac574-247">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ac574-247">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ac574-248">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ac574-248">Additional resources</span></span>

* [<span data-ttu-id="ac574-249">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ac574-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ac574-250">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ac574-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-itrp-tutorial/tutorial_general_203.png

