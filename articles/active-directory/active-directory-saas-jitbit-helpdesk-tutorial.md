---
title: "Samouczek: Integracji Azure Active Directory z pomocą techniczną Jitbit | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Jitbit pracy działu pomocy technicznej."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 0f6c837bbb910c1e84f7ed9da676c5ab40f75338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a><span data-ttu-id="0c0ec-103">Samouczek: Integracji Azure Active Directory z pomocą techniczną Jitbit</span><span class="sxs-lookup"><span data-stu-id="0c0ec-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span></span>

<span data-ttu-id="0c0ec-104">Z tego samouczka, dowiesz się, jak toointegrate Jitbit pracy działu pomocy technicznej w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0c0ec-104">In this tutorial, you learn how toointegrate Jitbit Helpdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0c0ec-105">Integrowanie pomocy technicznej Jitbit z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="0c0ec-105">Integrating Jitbit Helpdesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0c0ec-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooJitbit pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="0c0ec-106">You can control in Azure AD who has access tooJitbit Helpdesk</span></span>
- <span data-ttu-id="0c0ec-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooJitbit pomocy technicznej (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c0ec-107">You can enable your users tooautomatically get signed-on tooJitbit Helpdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0c0ec-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0c0ec-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="0c0ec-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0c0ec-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0c0ec-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0c0ec-110">Prerequisites</span></span>

<span data-ttu-id="0c0ec-111">tooconfigure integracji usługi Azure AD z pomocą techniczną Jitbit należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="0c0ec-111">tooconfigure Azure AD integration with Jitbit Helpdesk, you need hello following items:</span></span>

- <span data-ttu-id="0c0ec-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c0ec-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0c0ec-113">Pomoc techniczna Jitbit logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="0c0ec-113">A Jitbit Helpdesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0c0ec-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0c0ec-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="0c0ec-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0c0ec-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0c0ec-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0c0ec-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0c0ec-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="0c0ec-118">Scenario description</span></span>
<span data-ttu-id="0c0ec-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0c0ec-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="0c0ec-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0c0ec-121">Dodawanie pomocy technicznej Jitbit z galerii hello</span><span class="sxs-lookup"><span data-stu-id="0c0ec-121">Adding Jitbit Helpdesk from hello gallery</span></span>
2. <span data-ttu-id="0c0ec-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="0c0ec-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jitbit-helpdesk-from-hello-gallery"></a><span data-ttu-id="0c0ec-123">Dodawanie pomocy technicznej Jitbit z galerii hello</span><span class="sxs-lookup"><span data-stu-id="0c0ec-123">Adding Jitbit Helpdesk from hello gallery</span></span>
<span data-ttu-id="0c0ec-124">tooconfigure hello integracji Jitbit pracy działu pomocy technicznej usługi Azure AD, należy tooadd techniczną Jitbit z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-124">tooconfigure hello integration of Jitbit Helpdesk into Azure AD, you need tooadd Jitbit Helpdesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0c0ec-125">**tooadd techniczną Jitbit z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="0c0ec-125">**tooadd Jitbit Helpdesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0c0ec-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="0c0ec-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0c0ec-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="0c0ec-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="0c0ec-133">W polu wyszukiwania hello wpisz **techniczną Jitbit**.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-133">In hello search box, type **Jitbit Helpdesk**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. <span data-ttu-id="0c0ec-135">W panelu wyników hello, wybierz **techniczną Jitbit**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-135">In hello results panel, select **Jitbit Helpdesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0c0ec-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="0c0ec-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0c0ec-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z pomocą techniczną Jitbit w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-138">In this section, you configure and test Azure AD single sign-on with Jitbit Helpdesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0c0ec-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Jitbit pomoc techniczna jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Jitbit Helpdesk is tooa user in Azure AD.</span></span> <span data-ttu-id="0c0ec-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w pomocy technicznej Jitbit musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-140">In other words, a link relationship between an Azure AD user and hello related user in Jitbit Helpdesk needs toobe established.</span></span>

<span data-ttu-id="0c0ec-141">W pomocy technicznej Jitbit, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-141">In Jitbit Helpdesk, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="0c0ec-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z pomocą techniczną Jitbit, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="0c0ec-142">tooconfigure and test Azure AD single sign-on with Jitbit Helpdesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0c0ec-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0c0ec-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0c0ec-145">**[Tworzenie użytkownika testowego techniczną Jitbit](#creating-a-jitbit-helpdesk-test-user)**  -toohave odpowiednikiem Simona Britta w Jitbit pomocy technicznej, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-145">**[Creating a Jitbit Helpdesk test user](#creating-a-jitbit-helpdesk-test-user)** - toohave a counterpart of Britta Simon in Jitbit Helpdesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="0c0ec-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0c0ec-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0c0ec-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0c0ec-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0c0ec-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji Jitbit pracy działu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Jitbit Helpdesk application.</span></span>

<span data-ttu-id="0c0ec-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z pomocą techniczną Jitbit, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0c0ec-150">**tooconfigure Azure AD single sign-on with Jitbit Helpdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="0c0ec-151">W portalu Azure na powitania hello **techniczną Jitbit** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-151">In hello Azure portal, on hello **Jitbit Helpdesk** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="0c0ec-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. <span data-ttu-id="0c0ec-155">Na powitania **Jitbit pomoc techniczna domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="0c0ec-155">On hello **Jitbit Helpdesk Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    <span data-ttu-id="0c0ec-157">a.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-157">a.</span></span> <span data-ttu-id="0c0ec-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="0c0ec-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > <span data-ttu-id="0c0ec-159">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-159">This value is not real.</span></span> <span data-ttu-id="0c0ec-160">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-160">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="0c0ec-161">Skontaktuj się z [zespołem pomocy technicznej klienta techniczną Jitbit](https://www.jitbit.com/support/) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-161">Contact [Jitbit Helpdesk Client support team](https://www.jitbit.com/support/) tooget this value.</span></span> 
    
    <span data-ttu-id="0c0ec-162">b.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-162">b.</span></span>  <span data-ttu-id="0c0ec-163">W hello **identyfikator** tekstowym, wpisz adres URL jako poniżej:`https://www.jitbit.com/web-helpdesk/`</span><span class="sxs-lookup"><span data-stu-id="0c0ec-163">In hello **Identifier** textbox, type a URL as following: `https://www.jitbit.com/web-helpdesk/`</span></span>

    
 


4. <span data-ttu-id="0c0ec-164">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. <span data-ttu-id="0c0ec-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0c0ec-168">Na powitania **Jitbit pomoc techniczna konfiguracji** kliknij **skonfigurować Pomoc techniczna Jitbit** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-168">On hello **Jitbit Helpdesk Configuration** section, click **Configure Jitbit Helpdesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0c0ec-169">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="0c0ec-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. <span data-ttu-id="0c0ec-171">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny Jitbit pracy działu pomocy technicznej firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-171">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span></span>

8. <span data-ttu-id="0c0ec-172">Witaj pasku narzędzi u góry hello, kliknij przycisk **administracji**.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-172">In hello toolbar on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="0c0ec-173">![Administracja](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="0c0ec-173">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

9. <span data-ttu-id="0c0ec-174">Kliknij przycisk **ustawienia ogólne**.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-174">Click **General settings**.</span></span>
   
    <span data-ttu-id="0c0ec-175">![Użytkownicy, firm i uprawnienia](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "użytkowników, firmach i uprawnień")</span><span class="sxs-lookup"><span data-stu-id="0c0ec-175">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Users, companies, and permissions")</span></span>

10. <span data-ttu-id="0c0ec-176">W hello **ustawienia uwierzytelniania** konfiguracji sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="0c0ec-176">In hello **Authentication settings** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="0c0ec-177">![Ustawienia uwierzytelniania](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "ustawienia uwierzytelniania")</span><span class="sxs-lookup"><span data-stu-id="0c0ec-177">![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span></span>
    
    <span data-ttu-id="0c0ec-178">a.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-178">a.</span></span> <span data-ttu-id="0c0ec-179">Wybierz **Włącz SAML 2.0 pojedynczego logowania**, toosign za pomocą pojedynczego logowania jednokrotnego (SSO), z **OneLogin**.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-179">Select **Enable SAML 2.0 single sign on**, toosign in using Single Sign-On (SSO), with **OneLogin**.</span></span>

    <span data-ttu-id="0c0ec-180">b.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-180">b.</span></span> <span data-ttu-id="0c0ec-181">W hello **adres URL punktu końcowego** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-181">In hello **EndPoint URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="0c0ec-182">c.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-182">c.</span></span> <span data-ttu-id="0c0ec-183">Otwórz z **base-64** zakodowany certyfikat w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikatu X.509** pole tekstowe</span><span class="sxs-lookup"><span data-stu-id="0c0ec-183">Open your **base-64** encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>

    <span data-ttu-id="0c0ec-184">d.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-184">d.</span></span> <span data-ttu-id="0c0ec-185">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-185">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="0c0ec-186">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="0c0ec-186">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="0c0ec-187">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-187">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="0c0ec-188">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="0c0ec-188">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0c0ec-189">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c0ec-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="0c0ec-190">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-190">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="0c0ec-192">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0c0ec-192">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0c0ec-193">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-193">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0c0ec-195">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-195">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0c0ec-197">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-197">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0c0ec-199">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0c0ec-199">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0c0ec-201">a.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-201">a.</span></span> <span data-ttu-id="0c0ec-202">W hello **nazwa** pole tekstowe, nazwa typu jako **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-202">In hello **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="0c0ec-203">b.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-203">b.</span></span> <span data-ttu-id="0c0ec-204">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-204">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0c0ec-205">c.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-205">c.</span></span> <span data-ttu-id="0c0ec-206">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-206">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0c0ec-207">d.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-207">d.</span></span> <span data-ttu-id="0c0ec-208">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-208">Click **Create**.</span></span>
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a><span data-ttu-id="0c0ec-209">Tworzenie użytkownika testowego Jitbit pomoc techniczna</span><span class="sxs-lookup"><span data-stu-id="0c0ec-209">Creating a Jitbit Helpdesk test user</span></span>

<span data-ttu-id="0c0ec-210">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do pomocy technicznej Jitbit muszą mieć przydzielone do Jitbit pracy działu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-210">In order tooenable Azure AD users toolog into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span></span>  <span data-ttu-id="0c0ec-211">W przypadku hello Jitbit pracy działu pomocy technicznej Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-211">In hello case of Jitbit Helpdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="0c0ec-212">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="0c0ec-212">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="0c0ec-213">Zaloguj się za tooyour **techniczną Jitbit** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-213">Log in tooyour **Jitbit Helpdesk** tenant.</span></span>

2. <span data-ttu-id="0c0ec-214">W menu hello na górze hello, kliknij przycisk **administracji**.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-214">In hello menu on hello top, click **Administration**.</span></span>
   
    <span data-ttu-id="0c0ec-215">![Administracja](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "administracji")</span><span class="sxs-lookup"><span data-stu-id="0c0ec-215">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

3. <span data-ttu-id="0c0ec-216">Kliknij przycisk **użytkowników, firmach i uprawnienia**.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-216">Click **Users, companies and permissions**.</span></span>
   
    <span data-ttu-id="0c0ec-217">![Użytkownicy, firm i uprawnienia](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "użytkowników, firmach i uprawnień")</span><span class="sxs-lookup"><span data-stu-id="0c0ec-217">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Users, companies, and permissions")</span></span>

4. <span data-ttu-id="0c0ec-218">Kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-218">Click **Add user**.</span></span>
   
    <span data-ttu-id="0c0ec-219">![Dodaj użytkownika](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="0c0ec-219">![Add user](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Add user")</span></span>
   
5. <span data-ttu-id="0c0ec-220">W sekcji Tworzenie hello wpisz dane hello hello konto usługi Azure AD, które chcesz tooprovision w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="0c0ec-220">In hello Create section, type hello data of hello Azure AD account you want tooprovision as follows:</span></span>

    <span data-ttu-id="0c0ec-221">![Utwórz](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "tworzenie")</span><span class="sxs-lookup"><span data-stu-id="0c0ec-221">![Create](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Create")</span></span>
   
   <span data-ttu-id="0c0ec-222">a.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-222">a.</span></span> <span data-ttu-id="0c0ec-223">W hello **Username** pole tekstowe, typ **BrittaSimon**, hello nazwy użytkownika podanej hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-223">In hello **Username** textbox, type **BrittaSimon**, hello user name as in hello Azure portal.</span></span>

   <span data-ttu-id="0c0ec-224">b.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-224">b.</span></span> <span data-ttu-id="0c0ec-225">W hello **E-mail** polem tekstowym wiadomości e-mail typu hello użytkownika, takich jak  **BrittaSimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="0c0ec-225">In hello **Email** textbox, type email of hello user like **BrittaSimon@contoso.com**.</span></span>

   <span data-ttu-id="0c0ec-226">c.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-226">c.</span></span> <span data-ttu-id="0c0ec-227">W hello **imię** pole tekstowe, typ imię użytkownika hello, takich jak **Britta**.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-227">In hello **First Name** textbox, type first name of hello user like **Britta**.</span></span>

   <span data-ttu-id="0c0ec-228">d.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-228">d.</span></span> <span data-ttu-id="0c0ec-229">W hello **nazwisko** pole tekstowe, typ nazwisko użytkownika hello, takich jak **Simona**.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-229">In hello **Last Name** textbox, type last name of hello user like **Simon**.</span></span>
   
   <span data-ttu-id="0c0ec-230">e.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-230">e.</span></span> <span data-ttu-id="0c0ec-231">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-231">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="0c0ec-232">Możesz użyć innych techniczną Jitbit użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Pomoc techniczna Jitbit tooprovision kont użytkowników usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-232">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk tooprovision Azure AD user accounts.</span></span>
> 
        

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0c0ec-233">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0c0ec-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0c0ec-234">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooJitbit pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooJitbit Helpdesk.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="0c0ec-236">**tooassign tooJitbit Simona Britta pomocy technicznej, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="0c0ec-236">**tooassign Britta Simon tooJitbit Helpdesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="0c0ec-237">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="0c0ec-239">Z listy aplikacji hello wybierz **techniczną Jitbit**.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-239">In hello applications list, select **Jitbit Helpdesk**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. <span data-ttu-id="0c0ec-241">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="0c0ec-243">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-243">Click **Add** button.</span></span> <span data-ttu-id="0c0ec-244">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="0c0ec-246">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0c0ec-247">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0c0ec-248">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0c0ec-249">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0c0ec-249">Testing single sign-on</span></span>

<span data-ttu-id="0c0ec-250">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-250">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0c0ec-251">Po kliknięciu hello techniczną Jitbit kafelka w hello Panel dostępu, należy pobrać strony logowania aplikacji Jitbit pracy działu pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="0c0ec-251">When you click hello Jitbit Helpdesk tile in hello Access Panel, you should get login page of Jitbit Helpdesk application.</span></span>
<span data-ttu-id="0c0ec-252">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0c0ec-252">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0c0ec-253">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="0c0ec-253">Additional resources</span></span>

* [<span data-ttu-id="0c0ec-254">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0c0ec-254">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0c0ec-255">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0c0ec-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

