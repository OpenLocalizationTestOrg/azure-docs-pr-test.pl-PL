---
title: 'Samouczek: Integracji Azure Active Directory z BambooHR | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i BambooHR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f826b5d2-9c64-47df-bbbf-0adf9eb0fa71
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: jeedes
ms.openlocfilehash: f9083f846beb3a4bf4cebbf18b42aba2dfef2472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bamboohr"></a><span data-ttu-id="8559a-103">Samouczek: Integracji Azure Active Directory z BambooHR</span><span class="sxs-lookup"><span data-stu-id="8559a-103">Tutorial: Azure Active Directory integration with BambooHR</span></span>

<span data-ttu-id="8559a-104">Z tego samouczka, dowiesz się, jak toointegrate BambooHR w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8559a-104">In this tutorial, you learn how toointegrate BambooHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8559a-105">Integracja z usługą Azure AD BambooHR zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8559a-105">Integrating BambooHR with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8559a-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooBambooHR</span><span class="sxs-lookup"><span data-stu-id="8559a-106">You can control in Azure AD who has access tooBambooHR</span></span>
- <span data-ttu-id="8559a-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooBambooHR (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8559a-107">You can enable your users tooautomatically get signed-on tooBambooHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8559a-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8559a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8559a-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8559a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8559a-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8559a-110">Prerequisites</span></span>

<span data-ttu-id="8559a-111">tooconfigure integracji z usługą Azure AD z BambooHR należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8559a-111">tooconfigure Azure AD integration with BambooHR, you need hello following items:</span></span>

- <span data-ttu-id="8559a-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8559a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8559a-113">BambooHR jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8559a-113">A BambooHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8559a-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8559a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8559a-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8559a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8559a-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8559a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8559a-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8559a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8559a-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8559a-118">Scenario description</span></span>
<span data-ttu-id="8559a-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8559a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8559a-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8559a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8559a-121">Dodawanie BambooHR z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8559a-121">Adding BambooHR from hello gallery</span></span>
2. <span data-ttu-id="8559a-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8559a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bamboohr-from-hello-gallery"></a><span data-ttu-id="8559a-123">Dodawanie BambooHR z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8559a-123">Adding BambooHR from hello gallery</span></span>
<span data-ttu-id="8559a-124">tooconfigure hello integracji BambooHR do usługi Azure AD, należy tooadd BambooHR z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8559a-124">tooconfigure hello integration of BambooHR into Azure AD, you need tooadd BambooHR from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8559a-125">**tooadd BambooHR z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8559a-125">**tooadd BambooHR from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8559a-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8559a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="8559a-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8559a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8559a-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8559a-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="8559a-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8559a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="8559a-133">W polu wyszukiwania hello wpisz **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="8559a-133">In hello search box, type **BambooHR**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_search.png)

5. <span data-ttu-id="8559a-135">W panelu wyników hello zaznacz **BambooHR**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8559a-135">In hello results panel, select **BambooHR**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8559a-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8559a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8559a-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z BambooHR na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="8559a-138">In this section, you configure and test Azure AD single sign-on with BambooHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8559a-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w BambooHR jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8559a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BambooHR is tooa user in Azure AD.</span></span> <span data-ttu-id="8559a-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w BambooHR musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="8559a-140">In other words, a link relationship between an Azure AD user and hello related user in BambooHR needs toobe established.</span></span>

<span data-ttu-id="8559a-141">W BambooHR, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="8559a-141">In BambooHR, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8559a-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z BambooHR, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8559a-142">tooconfigure and test Azure AD single sign-on with BambooHR, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8559a-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="8559a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8559a-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8559a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8559a-145">**[Tworzenie użytkownika testowego BambooHR](#creating-a-bamboohr-test-user)**  -toohave odpowiednikiem Simona Britta w BambooHR, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8559a-145">**[Creating a BambooHR test user](#creating-a-bamboohr-test-user)** - toohave a counterpart of Britta Simon in BambooHR that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8559a-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8559a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8559a-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="8559a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8559a-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8559a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8559a-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji BambooHR.</span><span class="sxs-lookup"><span data-stu-id="8559a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BambooHR application.</span></span>

<span data-ttu-id="8559a-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z BambooHR, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8559a-150">**tooconfigure Azure AD single sign-on with BambooHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="8559a-151">W portalu Azure na powitania hello **BambooHR** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="8559a-151">In hello Azure portal, on hello **BambooHR** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="8559a-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8559a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_samlbase.png)

3. <span data-ttu-id="8559a-155">Na powitania **BambooHR domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8559a-155">On hello **BambooHR Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_url.png)

    <span data-ttu-id="8559a-157">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company>.bamboohr.com`</span><span class="sxs-lookup"><span data-stu-id="8559a-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.bamboohr.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="8559a-158">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="8559a-158">This value is not real.</span></span> <span data-ttu-id="8559a-159">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="8559a-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="8559a-160">Skontaktuj się z [zespołem pomocy technicznej klienta BambooHR](https://www.bamboohr.com/contact.php) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="8559a-160">Contact [BambooHR Client support team](https://www.bamboohr.com/contact.php) tooget this value.</span></span> 
 
4. <span data-ttu-id="8559a-161">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="8559a-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_certificate.png) 

5. <span data-ttu-id="8559a-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8559a-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8559a-165">Na powitania **konfiguracji BambooHR** kliknij **skonfigurować BambooHR** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="8559a-165">On hello **BambooHR Configuration** section, click **Configure BambooHR** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="8559a-166">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="8559a-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_configure.png) 

6. <span data-ttu-id="8559a-168">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy BambooHR jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8559a-168">In a different web browser window, log into your BambooHR company site as an administrator.</span></span>

7. <span data-ttu-id="8559a-169">Na głównej hello wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8559a-169">On hello homepage, perform hello following steps:</span></span>
   
    <span data-ttu-id="8559a-170">![Logowanie jednokrotne](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="8559a-170">![Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Single Sign-On")</span></span>   

    <span data-ttu-id="8559a-171">a.</span><span class="sxs-lookup"><span data-stu-id="8559a-171">a.</span></span> <span data-ttu-id="8559a-172">Kliknij przycisk **aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="8559a-172">Click **Apps**.</span></span>
   
    <span data-ttu-id="8559a-173">b.</span><span class="sxs-lookup"><span data-stu-id="8559a-173">b.</span></span> <span data-ttu-id="8559a-174">W menu aplikacji hello po lewej stronie powitania kliknij **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="8559a-174">In hello apps menu on hello left, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="8559a-175">c.</span><span class="sxs-lookup"><span data-stu-id="8559a-175">c.</span></span> <span data-ttu-id="8559a-176">Kliknij przycisk **SAML logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="8559a-176">Click **SAML Single Sign-On**.</span></span>

8. <span data-ttu-id="8559a-177">W hello **SAML logowania jednokrotnego** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8559a-177">In hello **SAML Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="8559a-178">![SAML logowania jednokrotnego](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML logowania jednokrotnego")</span><span class="sxs-lookup"><span data-stu-id="8559a-178">![SAML Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML Single Sign-On")</span></span>
   
    <span data-ttu-id="8559a-179">a.</span><span class="sxs-lookup"><span data-stu-id="8559a-179">a.</span></span> <span data-ttu-id="8559a-180">Wklej hello **SAML pojedynczy znak na adres URL usługi** wartości do hello **adres Url logowania jednokrotnego logowania** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8559a-180">Paste hello **SAML Single Sign-On Service URL** value into hello **SSO Login Url** textbox.</span></span>
      
    <span data-ttu-id="8559a-181">b.</span><span class="sxs-lookup"><span data-stu-id="8559a-181">b.</span></span> <span data-ttu-id="8559a-182">Otwórz zakodowanego certyfikatu base-64 pobrany z portalu Azure w programie Notatnik hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu X.509** pole tekstowe</span><span class="sxs-lookup"><span data-stu-id="8559a-182">Open base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>
   
    <span data-ttu-id="8559a-183">c.</span><span class="sxs-lookup"><span data-stu-id="8559a-183">c.</span></span> <span data-ttu-id="8559a-184">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="8559a-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="8559a-185">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="8559a-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8559a-186">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="8559a-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8559a-187">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8559a-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8559a-188">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8559a-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="8559a-189">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="8559a-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="8559a-191">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8559a-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8559a-192">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8559a-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8559a-194">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="8559a-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8559a-196">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8559a-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8559a-198">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8559a-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8559a-200">a.</span><span class="sxs-lookup"><span data-stu-id="8559a-200">a.</span></span> <span data-ttu-id="8559a-201">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8559a-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8559a-202">b.</span><span class="sxs-lookup"><span data-stu-id="8559a-202">b.</span></span> <span data-ttu-id="8559a-203">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8559a-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8559a-204">c.</span><span class="sxs-lookup"><span data-stu-id="8559a-204">c.</span></span> <span data-ttu-id="8559a-205">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="8559a-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8559a-206">d.</span><span class="sxs-lookup"><span data-stu-id="8559a-206">d.</span></span> <span data-ttu-id="8559a-207">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8559a-207">Click **Create**.</span></span>
 
### <a name="creating-a-bamboohr-test-user"></a><span data-ttu-id="8559a-208">Tworzenie użytkownika testowego BambooHR</span><span class="sxs-lookup"><span data-stu-id="8559a-208">Creating a BambooHR test user</span></span>

<span data-ttu-id="8559a-209">toolog użytkowników tooenable usługi Azure AD w tooBambooHR, muszą mieć przydzielone do BambooHR.</span><span class="sxs-lookup"><span data-stu-id="8559a-209">tooenable Azure AD users toolog in tooBambooHR, they must be provisioned into BambooHR.</span></span>  

<span data-ttu-id="8559a-210">W przypadku hello BambooHR Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="8559a-210">In hello case of BambooHR, provisioning is a manual task.</span></span>

<span data-ttu-id="8559a-211">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="8559a-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="8559a-212">Zaloguj się za tooyour **BambooHR** lokacji jako administrator.</span><span class="sxs-lookup"><span data-stu-id="8559a-212">Log in tooyour **BambooHR** site as administrator.</span></span>

2. <span data-ttu-id="8559a-213">Witaj pasku narzędzi u góry hello, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="8559a-213">In hello toolbar on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="8559a-214">![Ustawienie](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "ustawienie")</span><span class="sxs-lookup"><span data-stu-id="8559a-214">![Setting](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Setting")</span></span>

3. <span data-ttu-id="8559a-215">Kliknij przycisk **omówienie**.</span><span class="sxs-lookup"><span data-stu-id="8559a-215">Click **Overview**.</span></span>

4. <span data-ttu-id="8559a-216">W okienku nawigacji po lewej stronie powitania Przejdź zbyt**zabezpieczeń \> użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="8559a-216">In hello left navigation pane, go too**Security \> Users**.</span></span>

5. <span data-ttu-id="8559a-217">Wpisz nazwę użytkownika hello, hasło i adres e-mail prawidłowego konta usługi AAD, które chcesz tooprovision do hello związanych z pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="8559a-217">Type hello user name, password, and email address of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

6. <span data-ttu-id="8559a-218">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="8559a-218">Click **Save**.</span></span>
        
>[!NOTE]
><span data-ttu-id="8559a-219">Możesz użyć innych BambooHR użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez BambooHR tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="8559a-219">You can use any other BambooHR user account creation tools or APIs provided by BambooHR tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8559a-220">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8559a-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8559a-221">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooBambooHR.</span><span class="sxs-lookup"><span data-stu-id="8559a-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBambooHR.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="8559a-223">**tooassign tooBambooHR Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="8559a-223">**tooassign Britta Simon tooBambooHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="8559a-224">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8559a-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8559a-226">Z listy aplikacji hello wybierz **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="8559a-226">In hello applications list, select **BambooHR**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_app.png) 

3. <span data-ttu-id="8559a-228">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8559a-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="8559a-230">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8559a-230">Click **Add** button.</span></span> <span data-ttu-id="8559a-231">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8559a-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="8559a-233">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8559a-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8559a-234">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8559a-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8559a-235">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8559a-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8559a-236">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8559a-236">Testing single sign-on</span></span>

<span data-ttu-id="8559a-237">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8559a-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8559a-238">Po kliknięciu kafelka BambooHR hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour BambooHR aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8559a-238">When you click hello BambooHR tile in hello Access Panel, you should get automatically signed-on tooyour BambooHR application.</span></span>
<span data-ttu-id="8559a-239">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8559a-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8559a-240">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8559a-240">Additional resources</span></span>

* [<span data-ttu-id="8559a-241">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8559a-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8559a-242">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8559a-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_203.png

