---
title: 'Samouczek: Integracji Azure Active Directory z AppDynamics | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i AppDynamics."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 25fd1df0-411c-4f55-8be3-4273b543100f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9b63afec73d7442e6ac1ce34b511beea6f43ffe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appdynamics"></a><span data-ttu-id="b9a6a-103">Samouczek: Integracji Azure Active Directory z AppDynamics</span><span class="sxs-lookup"><span data-stu-id="b9a6a-103">Tutorial: Azure Active Directory integration with AppDynamics</span></span>

<span data-ttu-id="b9a6a-104">Z tego samouczka, dowiesz się, jak toointegrate AppDynamics w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b9a6a-104">In this tutorial, you learn how toointegrate AppDynamics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b9a6a-105">Integracja z usługą Azure AD AppDynamics zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="b9a6a-105">Integrating AppDynamics with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b9a6a-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooAppDynamics</span><span class="sxs-lookup"><span data-stu-id="b9a6a-106">You can control in Azure AD who has access tooAppDynamics</span></span>
- <span data-ttu-id="b9a6a-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAppDynamics (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9a6a-107">You can enable your users tooautomatically get signed-on tooAppDynamics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b9a6a-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b9a6a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b9a6a-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b9a6a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9a6a-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b9a6a-110">Prerequisites</span></span>

<span data-ttu-id="b9a6a-111">tooconfigure integracji z usługą Azure AD z AppDynamics należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b9a6a-111">tooconfigure Azure AD integration with AppDynamics, you need hello following items:</span></span>

- <span data-ttu-id="b9a6a-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9a6a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b9a6a-113">AppDynamics logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b9a6a-113">An AppDynamics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b9a6a-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b9a6a-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="b9a6a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9a6a-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b9a6a-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9a6a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b9a6a-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="b9a6a-118">Scenario description</span></span>
<span data-ttu-id="b9a6a-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b9a6a-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="b9a6a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9a6a-121">Dodawanie AppDynamics z galerii hello</span><span class="sxs-lookup"><span data-stu-id="b9a6a-121">Adding AppDynamics from hello gallery</span></span>
2. <span data-ttu-id="b9a6a-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b9a6a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appdynamics-from-hello-gallery"></a><span data-ttu-id="b9a6a-123">Dodawanie AppDynamics z galerii hello</span><span class="sxs-lookup"><span data-stu-id="b9a6a-123">Adding AppDynamics from hello gallery</span></span>
<span data-ttu-id="b9a6a-124">tooconfigure hello integracji AppDynamics do usługi Azure AD, należy tooadd AppDynamics z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-124">tooconfigure hello integration of AppDynamics into Azure AD, you need tooadd AppDynamics from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b9a6a-125">**tooadd AppDynamics z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b9a6a-125">**tooadd AppDynamics from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9a6a-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="b9a6a-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b9a6a-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="b9a6a-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="b9a6a-133">W polu wyszukiwania hello wpisz **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-133">In hello search box, type **AppDynamics**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_search.png)

5. <span data-ttu-id="b9a6a-135">W panelu wyników hello zaznacz **AppDynamics**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-135">In hello results panel, select **AppDynamics**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b9a6a-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b9a6a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b9a6a-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z AppDynamics na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="b9a6a-138">In this section, you configure and test Azure AD single sign-on with AppDynamics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b9a6a-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w AppDynamics jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in AppDynamics is tooa user in Azure AD.</span></span> <span data-ttu-id="b9a6a-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w AppDynamics musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-140">In other words, a link relationship between an Azure AD user and hello related user in AppDynamics needs toobe established.</span></span>

<span data-ttu-id="b9a6a-141">W AppDynamics, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-141">In AppDynamics, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b9a6a-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z AppDynamics, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b9a6a-142">tooconfigure and test Azure AD single sign-on with AppDynamics, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b9a6a-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b9a6a-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b9a6a-145">**[Tworzenie użytkownika testowego AppDynamics](#creating-an-appdynamics-test-user)**  -toohave odpowiednikiem Simona Britta w AppDynamics, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-145">**[Creating an AppDynamics test user](#creating-an-appdynamics-test-user)** - toohave a counterpart of Britta Simon in AppDynamics that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b9a6a-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b9a6a-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b9a6a-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b9a6a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b9a6a-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your AppDynamics application.</span></span>

<span data-ttu-id="b9a6a-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z AppDynamics, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b9a6a-150">**tooconfigure Azure AD single sign-on with AppDynamics, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9a6a-151">W portalu Azure na powitania hello **AppDynamics** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-151">In hello Azure portal, on hello **AppDynamics** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="b9a6a-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_samlbase.png)

3. <span data-ttu-id="b9a6a-155">Na powitania **AppDynamics domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="b9a6a-155">On hello **AppDynamics Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_url.png)

    <span data-ttu-id="b9a6a-157">a.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-157">a.</span></span> <span data-ttu-id="b9a6a-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.saas.appdynamics.com`</span><span class="sxs-lookup"><span data-stu-id="b9a6a-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.saas.appdynamics.com`</span></span>

    <span data-ttu-id="b9a6a-159">b.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-159">b.</span></span> <span data-ttu-id="b9a6a-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.saas.appdynamics.com/controller`</span><span class="sxs-lookup"><span data-stu-id="b9a6a-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.saas.appdynamics.com/controller`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b9a6a-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-161">These values are not real.</span></span> <span data-ttu-id="b9a6a-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b9a6a-163">Skontaktuj się z [zespołem pomocy technicznej klienta AppDynamics](https://www.appdynamics.com/support/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-163">Contact [AppDynamics Client support team](https://www.appdynamics.com/support/) tooget these values.</span></span> 
 
4. <span data-ttu-id="b9a6a-164">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_certificate.png) 

5. <span data-ttu-id="b9a6a-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appdynamics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b9a6a-168">Na powitania **konfiguracji AppDynamics** kliknij **skonfigurować AppDynamics** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-168">On hello **AppDynamics Configuration** section, click **Configure AppDynamics** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b9a6a-169">Witaj kopii **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="b9a6a-169">Copy hello **Sign-Out URL, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_configure.png) 

7. <span data-ttu-id="b9a6a-171">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy AppDynamics tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-171">In a different web browser window, log in tooyour AppDynamics company site as an administrator.</span></span>

8. <span data-ttu-id="b9a6a-172">Witaj pasku narzędzi u góry hello, kliknij przycisk **ustawienia**, a następnie kliknij przycisk **administracji**.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-172">In hello toolbar on hello top, click **Settings**, and then click **Administration**.</span></span>
   
    <span data-ttu-id="b9a6a-173">![Administracja](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="b9a6a-173">![Administration](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administration")</span></span>

9. <span data-ttu-id="b9a6a-174">Kliknij przycisk hello **dostawcy uwierzytelniania** kartę.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-174">Click hello **Authentication Provider** tab.</span></span>
   
    <span data-ttu-id="b9a6a-175">![Dostawca uwierzytelniania](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "dostawcy uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="b9a6a-175">![Authentication Provider](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Authentication Provider")</span></span>

10. <span data-ttu-id="b9a6a-176">W hello **dostawcy uwierzytelniania** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="b9a6a-176">In hello **Authentication Provider** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="b9a6a-177">![Konfiguracja SAML](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "Konfiguracja SAML")</span><span class="sxs-lookup"><span data-stu-id="b9a6a-177">![SAML Configuration](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML Configuration")</span></span>   

    <span data-ttu-id="b9a6a-178">a.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-178">a.</span></span> <span data-ttu-id="b9a6a-179">Jako **dostawcy uwierzytelniania**, wybierz pozycję **SAML**.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-179">As **Authentication Provider**, select **SAML**.</span></span>

    <span data-ttu-id="b9a6a-180">b.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-180">b.</span></span> <span data-ttu-id="b9a6a-181">W hello **adres URL logowania** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-181">In hello **Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b9a6a-182">c.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-182">c.</span></span> <span data-ttu-id="b9a6a-183">W hello **adresu URL wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-183">In hello **Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="b9a6a-184">d.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-184">d.</span></span> <span data-ttu-id="b9a6a-185">Otwieranie certyfikatu zakodowanego base-64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu** pole tekstowe</span><span class="sxs-lookup"><span data-stu-id="b9a6a-185">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Certificate** textbox</span></span>

    <span data-ttu-id="b9a6a-186">e.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-186">e.</span></span> <span data-ttu-id="b9a6a-187">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-187">Click **Save**.</span></span>

     <span data-ttu-id="b9a6a-188">![Zapisz](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Zapisz")</span><span class="sxs-lookup"><span data-stu-id="b9a6a-188">![Save](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Save")</span></span>

> [!TIP]
> <span data-ttu-id="b9a6a-189">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="b9a6a-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b9a6a-190">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b9a6a-191">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b9a6a-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b9a6a-192">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9a6a-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="b9a6a-193">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="b9a6a-195">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b9a6a-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9a6a-196">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b9a6a-198">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b9a6a-200">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b9a6a-202">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b9a6a-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b9a6a-204">a.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-204">a.</span></span> <span data-ttu-id="b9a6a-205">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9a6a-206">b.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-206">b.</span></span> <span data-ttu-id="b9a6a-207">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b9a6a-208">c.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-208">c.</span></span> <span data-ttu-id="b9a6a-209">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b9a6a-210">d.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-210">d.</span></span> <span data-ttu-id="b9a6a-211">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-211">Click **Create**.</span></span>
 
### <a name="creating-an-appdynamics-test-user"></a><span data-ttu-id="b9a6a-212">Tworzenie użytkownika testowego AppDynamics</span><span class="sxs-lookup"><span data-stu-id="b9a6a-212">Creating an AppDynamics test user</span></span>

<span data-ttu-id="b9a6a-213">toolog użytkowników tooenable usługi Azure AD w tooAppDynamics, muszą mieć przydzielone do AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-213">tooenable Azure AD users toolog in tooAppDynamics, they must be provisioned into AppDynamics.</span></span> <span data-ttu-id="b9a6a-214">W przypadku hello AppDynamics Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-214">In hello case of AppDynamics, provisioning is a manual task.</span></span>

<span data-ttu-id="b9a6a-215">**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b9a6a-215">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9a6a-216">Zaloguj się za tooyour AppDynamics witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-216">Log in tooyour AppDynamics company site as an administrator.</span></span>

2. <span data-ttu-id="b9a6a-217">Przejdź za**użytkowników**, a następnie kliknij przycisk  **+**  tooopen hello **Tworzenie użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-217">Go too**Users**, and then click **+** tooopen hello **Create User** dialog.</span></span>
   
    <span data-ttu-id="b9a6a-218">![Użytkownicy](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="b9a6a-218">![Users](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Users")</span></span>

3. <span data-ttu-id="b9a6a-219">W hello **Tworzenie użytkownika** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="b9a6a-219">In hello **Create User** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="b9a6a-220">![Utwórz użytkownika](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Tworzenie użytkownika")</span><span class="sxs-lookup"><span data-stu-id="b9a6a-220">![Create User](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Create User")</span></span>
   
    <span data-ttu-id="b9a6a-221">a.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-221">a.</span></span> <span data-ttu-id="b9a6a-222">Typ hello **Username**, **nazwa**, **poczty E-mail**, **nowe hasło**, **powtórz nowe hasło** z prawidłową usługi AAD konto ma tooprovision do hello związane z pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-222">Type hello **Username**, **Name**, **Email**, **New Password**, **Repeat New Password** of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

    <span data-ttu-id="b9a6a-223">b.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-223">b.</span></span> <span data-ttu-id="b9a6a-224">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-224">Click **Save**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="b9a6a-225">Możesz użyć innych AppDynamics użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez AppDynamics tooprovision kont użytkowników usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-225">You can use any other AppDynamics user account creation tools or APIs provided by AppDynamics tooprovision Azure AD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b9a6a-226">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9a6a-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b9a6a-227">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAppDynamics.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAppDynamics.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="b9a6a-229">**tooassign tooAppDynamics Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b9a6a-229">**tooassign Britta Simon tooAppDynamics, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9a6a-230">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="b9a6a-232">Z listy aplikacji hello wybierz **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-232">In hello applications list, select **AppDynamics**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_app.png) 

3. <span data-ttu-id="b9a6a-234">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="b9a6a-236">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-236">Click **Add** button.</span></span> <span data-ttu-id="b9a6a-237">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="b9a6a-239">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b9a6a-240">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b9a6a-241">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b9a6a-242">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b9a6a-242">Testing single sign-on</span></span>

<span data-ttu-id="b9a6a-243">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b9a6a-244">Po kliknięciu powitalne AppDynamics kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour AppDynamics aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b9a6a-244">When you click hello AppDynamics tile in hello Access Panel, you should get automatically signed-on tooyour AppDynamics application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b9a6a-245">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b9a6a-245">Additional resources</span></span>

* [<span data-ttu-id="b9a6a-246">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b9a6a-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b9a6a-247">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b9a6a-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_203.png

