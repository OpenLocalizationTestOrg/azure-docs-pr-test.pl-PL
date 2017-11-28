---
title: 'Samouczek: Integracji Azure Active Directory z Panorama9 | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Panorama9."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e28d7fa-03be-49f3-96c8-b567f1257d44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 548fb6434d920e076db98a0193f8dfdf8a958a91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panorama9"></a><span data-ttu-id="8d1d6-103">Samouczek: Integracji Azure Active Directory z Panorama9</span><span class="sxs-lookup"><span data-stu-id="8d1d6-103">Tutorial: Azure Active Directory integration with Panorama9</span></span>

<span data-ttu-id="8d1d6-104">Z tego samouczka, dowiesz się, jak toointegrate Panorama9 w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8d1d6-104">In this tutorial, you learn how toointegrate Panorama9 with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8d1d6-105">Integracja z usługą Azure AD Panorama9 zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8d1d6-105">Integrating Panorama9 with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8d1d6-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooPanorama9</span><span class="sxs-lookup"><span data-stu-id="8d1d6-106">You can control in Azure AD who has access tooPanorama9</span></span>
- <span data-ttu-id="8d1d6-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPanorama9 (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d1d6-107">You can enable your users tooautomatically get signed-on tooPanorama9 (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8d1d6-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8d1d6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8d1d6-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8d1d6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8d1d6-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8d1d6-110">Prerequisites</span></span>

<span data-ttu-id="8d1d6-111">tooconfigure integracji z usługą Azure AD z Panorama9 należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8d1d6-111">tooconfigure Azure AD integration with Panorama9, you need hello following items:</span></span>

- <span data-ttu-id="8d1d6-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d1d6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8d1d6-113">Panorama9 logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8d1d6-113">A Panorama9 single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8d1d6-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8d1d6-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8d1d6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8d1d6-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8d1d6-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8d1d6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8d1d6-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8d1d6-118">Scenario description</span></span>
<span data-ttu-id="8d1d6-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8d1d6-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8d1d6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8d1d6-121">Dodawanie Panorama9 z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8d1d6-121">Adding Panorama9 from hello gallery</span></span>
2. <span data-ttu-id="8d1d6-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8d1d6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panorama9-from-hello-gallery"></a><span data-ttu-id="8d1d6-123">Dodawanie Panorama9 z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8d1d6-123">Adding Panorama9 from hello gallery</span></span>
<span data-ttu-id="8d1d6-124">tooconfigure hello integracji Panorama9 do usługi Azure AD, należy tooadd Panorama9 z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-124">tooconfigure hello integration of Panorama9 into Azure AD, you need tooadd Panorama9 from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8d1d6-125">**tooadd Panorama9 z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8d1d6-125">**tooadd Panorama9 from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d1d6-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="8d1d6-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8d1d6-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="8d1d6-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="8d1d6-133">W polu wyszukiwania hello wpisz **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-133">In hello search box, type **Panorama9**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_search.png)

5. <span data-ttu-id="8d1d6-135">W panelu wyników hello zaznacz **Panorama9**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-135">In hello results panel, select **Panorama9**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8d1d6-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8d1d6-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="8d1d6-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Panorama9 na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="8d1d6-138">In this section, you configure and test Azure AD single sign-on with Panorama9 based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8d1d6-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Panorama9 jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Panorama9 is tooa user in Azure AD.</span></span> <span data-ttu-id="8d1d6-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Panorama9 musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-140">In other words, a link relationship between an Azure AD user and hello related user in Panorama9 needs toobe established.</span></span>

<span data-ttu-id="8d1d6-141">W Panorama9, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-141">In Panorama9, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8d1d6-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Panorama9, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8d1d6-142">tooconfigure and test Azure AD single sign-on with Panorama9, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8d1d6-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8d1d6-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8d1d6-145">**[Tworzenie użytkownika testowego Panorama9](#creating-a-panorama9-test-user)**  -toohave odpowiednikiem Simona Britta w Panorama9, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-145">**[Creating a Panorama9 test user](#creating-a-panorama9-test-user)** - toohave a counterpart of Britta Simon in Panorama9 that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8d1d6-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8d1d6-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8d1d6-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8d1d6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8d1d6-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Panorama9.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Panorama9 application.</span></span>

<span data-ttu-id="8d1d6-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Panorama9, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8d1d6-150">**tooconfigure Azure AD single sign-on with Panorama9, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d1d6-151">W portalu Azure na powitania hello **Panorama9** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-151">In hello Azure portal, on hello **Panorama9** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="8d1d6-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_samlbase.png)

3. <span data-ttu-id="8d1d6-155">Na powitania **Panorama9 domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8d1d6-155">On hello **Panorama9 Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_url.png)

    <span data-ttu-id="8d1d6-157">a.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-157">a.</span></span> <span data-ttu-id="8d1d6-158">W hello **adres URL logowania** tekstowym, wpisz adres URL jako:`https://dashboard.panorama9.com/saml/access/3262`</span><span class="sxs-lookup"><span data-stu-id="8d1d6-158">In hello **Sign-on URL** textbox, type a URL as: `https://dashboard.panorama9.com/saml/access/3262`</span></span>

    <span data-ttu-id="8d1d6-159">b.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-159">b.</span></span> <span data-ttu-id="8d1d6-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`http://www.panorama9.com/saml20/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="8d1d6-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://www.panorama9.com/saml20/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8d1d6-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-161">These values are not real.</span></span> <span data-ttu-id="8d1d6-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8d1d6-163">Skontaktuj się z [zespołem pomocy technicznej klienta Panorama9](https://support.panorama9.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-163">Contact [Panorama9 Client support team](https://support.panorama9.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="8d1d6-164">Na powitania **certyfikat podpisywania SAML** hello kopiowania, sekcji **odcisk PALCA** wartości certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-164">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_certificate.png) 

5. <span data-ttu-id="8d1d6-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panorama9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8d1d6-168">Na powitania **konfiguracji Panorama9** kliknij **skonfigurować Panorama9** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-168">On hello **Panorama9 Configuration** section, click **Configure Panorama9** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8d1d6-169">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="8d1d6-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_configure.png) 

5. <span data-ttu-id="8d1d6-171">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Panorama9 jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-171">In a different web browser window, log into your Panorama9 company site as an administrator.</span></span>

6. <span data-ttu-id="8d1d6-172">Witaj pasku narzędzi u góry hello, kliknij przycisk **Zarządzaj**, a następnie kliknij przycisk **rozszerzenia**.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-172">In hello toolbar on hello top, click **Manage**, and then click **Extensions**.</span></span>
   
   <span data-ttu-id="8d1d6-173">![Rozszerzenia](./media/active-directory-saas-panorama9-tutorial/ic790023.png "rozszerzeń")</span><span class="sxs-lookup"><span data-stu-id="8d1d6-173">![Extensions](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Extensions")</span></span>
7. <span data-ttu-id="8d1d6-174">Na powitania **rozszerzenia** okna dialogowego, kliknij przycisk **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-174">On hello **Extensions** dialog, click **Single Sign-On**.</span></span>
   
   <span data-ttu-id="8d1d6-175">![Logowanie jednokrotne](./media/active-directory-saas-panorama9-tutorial/ic790024.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="8d1d6-175">![Single Sign-On](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Single Sign-On")</span></span>
8. <span data-ttu-id="8d1d6-176">W hello **ustawienia** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8d1d6-176">In hello **Settings** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="8d1d6-177">![Ustawienia](./media/active-directory-saas-panorama9-tutorial/ic790025.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="8d1d6-177">![Settings](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Settings")</span></span>
   
    <span data-ttu-id="8d1d6-178">a.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-178">a.</span></span> <span data-ttu-id="8d1d6-179">W **adres URL dostawcy tożsamości** pole tekstowe, Wklej wartość hello **pojedynczy znak na adres URL usługi**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-179">In **Identity provider URL** textbox, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="8d1d6-180">b.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-180">b.</span></span> <span data-ttu-id="8d1d6-181">W **odcisk palca certyfikatu** pole tekstowe, Wklej hello **odcisk palca** wartość certyfikatów, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-181">In **Certificate fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>    
         
9. <span data-ttu-id="8d1d6-182">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-182">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="8d1d6-183">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="8d1d6-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8d1d6-184">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8d1d6-185">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8d1d6-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8d1d6-186">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d1d6-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="8d1d6-187">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="8d1d6-189">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8d1d6-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d1d6-190">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8d1d6-192">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8d1d6-194">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8d1d6-196">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8d1d6-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8d1d6-198">a.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-198">a.</span></span> <span data-ttu-id="8d1d6-199">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8d1d6-200">b.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-200">b.</span></span> <span data-ttu-id="8d1d6-201">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8d1d6-202">c.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-202">c.</span></span> <span data-ttu-id="8d1d6-203">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8d1d6-204">d.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-204">d.</span></span> <span data-ttu-id="8d1d6-205">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-205">Click **Create**.</span></span>
 
### <a name="creating-a-panorama9-test-user"></a><span data-ttu-id="8d1d6-206">Tworzenie użytkownika testowego Panorama9</span><span class="sxs-lookup"><span data-stu-id="8d1d6-206">Creating a Panorama9 test user</span></span>

<span data-ttu-id="8d1d6-207">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Panorama9 muszą mieć przydzielone do Panorama9.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-207">In order tooenable Azure AD users toolog into Panorama9, they must be provisioned into Panorama9.</span></span>  

<span data-ttu-id="8d1d6-208">W przypadku hello Panorama9 Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-208">In hello case of Panorama9, provisioning is a manual task.</span></span>

<span data-ttu-id="8d1d6-209">**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8d1d6-209">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d1d6-210">Zaloguj się za tooyour **Panorama9** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-210">Log in tooyour **Panorama9** company site as an administrator.</span></span>

2. <span data-ttu-id="8d1d6-211">W menu hello na górze hello, kliknij przycisk **Zarządzaj**, a następnie kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-211">In hello menu on hello top, click **Manage**, and then click **Users**.</span></span>
   
  <span data-ttu-id="8d1d6-212">![Użytkownicy](./media/active-directory-saas-panorama9-tutorial/ic790027.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="8d1d6-212">![Users](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Users")</span></span>

3. <span data-ttu-id="8d1d6-213">W sekcji użytkownicy hello, kliknij przycisk  **+**  tooadd nowego użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-213">In hello Users section, Click **+** tooadd new user.</span></span>

 <span data-ttu-id="8d1d6-214">![Użytkownicy](./media/active-directory-saas-panorama9-tutorial/ic790028.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="8d1d6-214">![Users](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Users")</span></span>

4. <span data-ttu-id="8d1d6-215">Przejdź toohello sekcji danych użytkownika, typu hello adres e-mail z prawidłowym użytkownikiem usługi Azure Active Directory ma tooprovision do hello **E-mail** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-215">Go toohello User data section, type hello email address of a valid Azure Active Directory user you want tooprovision into hello **Email** textbox.</span></span>

5. <span data-ttu-id="8d1d6-216">Pochodzić toohello sekcji Użytkownicy kliknij **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-216">Come toohello Users section, Click **Save**.</span></span>
   
> [!NOTE]
    > <span data-ttu-id="8d1d6-217">Właściciel konta usługi Azure Active Directory Hello otrzymuje wiadomość e-mail i następuje tooconfirm łącze swojego konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-217">hello Azure Active Directory account holder receives an email and follows a link tooconfirm their account before it becomes active.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8d1d6-218">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d1d6-218">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8d1d6-219">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooPanorama9.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-219">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPanorama9.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="8d1d6-221">**tooassign tooPanorama9 Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="8d1d6-221">**tooassign Britta Simon tooPanorama9, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d1d6-222">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-222">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8d1d6-224">Z listy aplikacji hello wybierz **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-224">In hello applications list, select **Panorama9**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_app.png) 

3. <span data-ttu-id="8d1d6-226">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-226">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="8d1d6-228">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-228">Click **Add** button.</span></span> <span data-ttu-id="8d1d6-229">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="8d1d6-231">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-231">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8d1d6-232">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8d1d6-233">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8d1d6-234">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8d1d6-234">Testing single sign-on</span></span>

<span data-ttu-id="8d1d6-235">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-235">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8d1d6-236">Po kliknięciu kafelka hello Panorama9 w hello Panel dostępu, należy pobrać automatycznie zalogowane tooPanorama9 aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8d1d6-236">When you click hello Panorama9 tile in hello Access Panel, you should get automatically signed-on tooPanorama9 application.</span></span>
<span data-ttu-id="8d1d6-237">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8d1d6-237">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8d1d6-238">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8d1d6-238">Additional resources</span></span>

* [<span data-ttu-id="8d1d6-239">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8d1d6-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8d1d6-240">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8d1d6-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_203.png

