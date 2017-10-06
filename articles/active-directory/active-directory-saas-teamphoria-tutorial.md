---
title: 'Samouczek: Integracji Azure Active Directory z Teamphoria | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Teamphoria."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d569c705-6f0f-4ec1-b485-ba82526b5d32
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jeedes
ms.openlocfilehash: f32be9742b76f7fe464036dadc108c62e4a787a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-teamphoria"></a><span data-ttu-id="b9653-103">Samouczek: Integracji Azure Active Directory z Teamphoria</span><span class="sxs-lookup"><span data-stu-id="b9653-103">Tutorial: Azure Active Directory integration with Teamphoria</span></span>

<span data-ttu-id="b9653-104">Z tego samouczka, dowiesz się, jak toointegrate Teamphoria w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b9653-104">In this tutorial, you learn how toointegrate Teamphoria with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b9653-105">Integracja z usługą Azure AD Teamphoria zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="b9653-105">Integrating Teamphoria with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b9653-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooTeamphoria</span><span class="sxs-lookup"><span data-stu-id="b9653-106">You can control in Azure AD who has access tooTeamphoria</span></span>
- <span data-ttu-id="b9653-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooTeamphoria (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9653-107">You can enable your users tooautomatically get signed-on tooTeamphoria (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b9653-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="b9653-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="b9653-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b9653-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Teamphoria, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Teamphoria.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="b9653-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b9653-110">Prerequisites</span></span>

<span data-ttu-id="b9653-111">tooconfigure integracji z usługą Azure AD z Teamphoria należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b9653-111">tooconfigure Azure AD integration with Teamphoria, you need hello following items:</span></span>

- <span data-ttu-id="b9653-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9653-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b9653-113">Teamphoria jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b9653-113">A Teamphoria single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b9653-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b9653-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b9653-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="b9653-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9653-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b9653-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="b9653-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9653-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b9653-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="b9653-118">Scenario description</span></span>
<span data-ttu-id="b9653-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="b9653-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b9653-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="b9653-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9653-121">Dodawanie Teamphoria z galerii hello</span><span class="sxs-lookup"><span data-stu-id="b9653-121">Adding Teamphoria from hello gallery</span></span>
2. <span data-ttu-id="b9653-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b9653-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-teamphoria-from-hello-gallery"></a><span data-ttu-id="b9653-123">Dodawanie Teamphoria z galerii hello</span><span class="sxs-lookup"><span data-stu-id="b9653-123">Adding Teamphoria from hello gallery</span></span>
<span data-ttu-id="b9653-124">tooconfigure hello integracji Teamphoria do usługi Azure AD, należy tooadd Teamphoria z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="b9653-124">tooconfigure hello integration of Teamphoria into Azure AD, you need tooadd Teamphoria from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b9653-125">**tooadd Teamphoria z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b9653-125">**tooadd Teamphoria from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9653-126">W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b9653-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="b9653-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="b9653-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b9653-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b9653-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="b9653-131">Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b9653-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="b9653-133">W polu wyszukiwania hello wpisz **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="b9653-133">In hello search box, type **Teamphoria**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_search.png)

5. <span data-ttu-id="b9653-135">W panelu wyników hello zaznacz **Teamphoria**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="b9653-135">In hello results panel, select **Teamphoria**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b9653-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b9653-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b9653-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Teamphoria w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="b9653-138">In this section, you configure and test Azure AD single sign-on with Teamphoria based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b9653-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Teamphoria jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9653-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Teamphoria is tooa user in Azure AD.</span></span> <span data-ttu-id="b9653-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Teamphoria musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="b9653-140">In other words, a link relationship between an Azure AD user and hello related user in Teamphoria needs toobe established.</span></span>

<span data-ttu-id="b9653-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="b9653-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Teamphoria.</span></span>

<span data-ttu-id="b9653-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Teamphoria, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b9653-142">tooconfigure and test Azure AD single sign-on with Teamphoria, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b9653-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b9653-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b9653-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b9653-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b9653-145">**[Tworzenie użytkownika testowego Teamphoria](#creating-a-teamphoria-test-user)**  -toohave odpowiednikiem Simona Britta w Teamphoria, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9653-145">**[Creating a Teamphoria test user](#creating-a-teamphoria-test-user)** - toohave a counterpart of Britta Simon in Teamphoria that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="b9653-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b9653-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b9653-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="b9653-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b9653-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b9653-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b9653-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="b9653-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Teamphoria application.</span></span>

<span data-ttu-id="b9653-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Teamphoria, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b9653-150">**tooconfigure Azure AD single sign-on with Teamphoria, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9653-151">W portalu zarządzania Azure hello na powitania **Teamphoria** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="b9653-151">In hello Azure Management portal, on hello **Teamphoria** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="b9653-153">Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="b9653-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_samlbase.png)

3. <span data-ttu-id="b9653-155">Na powitania **Teamphoria domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="b9653-155">On hello **Teamphoria Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_url.png)

    <span data-ttu-id="b9653-157">a.</span><span class="sxs-lookup"><span data-stu-id="b9653-157">a.</span></span> <span data-ttu-id="b9653-158">W hello **adres URL logowania** pole tekstowe, wprowadź adres URL hello przy użyciu hello następującego wzorca:`https://<sub-domain>.teamphoria.com/login`</span><span class="sxs-lookup"><span data-stu-id="b9653-158">In hello **Sign-on URL** textbox, type hello URL using hello following pattern: `https://<sub-domain>.teamphoria.com/login`</span></span>  

    > [!NOTE] 
    > <span data-ttu-id="b9653-159">Należy pamiętać, że nie są one hello wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="b9653-159">Please note that these are not hello real values.</span></span> <span data-ttu-id="b9653-160">Masz tooupdate tych wartości za pomocą hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="b9653-160">You have tooupdate these values with hello actual Sign-On URL.</span></span> <span data-ttu-id="b9653-161">Skontaktuj się z [zespołem pomocy technicznej klienta Teamphoria](https://www.teamphoria.com/) tooget URL hello logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="b9653-161">Contact [Teamphoria Client support team](https://www.teamphoria.com/) tooget hello Sign-on URL.</span></span> 

4. <span data-ttu-id="b9653-162">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie Zapisz certyfikat hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b9653-162">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_certificate.png) 

5. <span data-ttu-id="b9653-164">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b9653-164">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b9653-166">Na powitania **konfiguracji Teamphoria** kliknij **skonfigurować Teamphoria** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="b9653-166">On hello **Teamphoria Configuration** section, click **Configure Teamphoria** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b9653-167">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="b9653-167">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_configure.png) 

7. <span data-ttu-id="b9653-169">tooconfigure rejestracji jednokrotnej w **Teamphoria** strona, logowania tooyour Teamphoria aplikacji jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b9653-169">tooconfigure single sign-on on **Teamphoria** side, Login tooyour Teamphoria application as an administrator.</span></span>

8. <span data-ttu-id="b9653-170">Przejdź za**ustawienia administratora** opcji hello lewym pasku narzędzi i w obszarze hello powitania kliknij kartę skonfigurować **POJEDYNCZEGO logowania** tooopen hello logowania jednokrotnego konfiguracji okna.</span><span class="sxs-lookup"><span data-stu-id="b9653-170">Go too**ADMIN SETTINGS** option in hello left toolbar and under hello hello Configure Tab click on **SINGLE SIGN-ON** tooopen hello SSO configuration window.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/admin_sso_configure.png)

9. <span data-ttu-id="b9653-172">Polecenie **Dodaj nowego DOSTAWCĘ tożsamości** opcję hello prawym górnym rogu tooopen hello formularz służący do dodawania hello ustawienia logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="b9653-172">Click on **ADD NEW IDENTITY PROVIDER** option in hello top right corner tooopen hello form for adding hello settings for SSO.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/add_new_identity_provider.png)

10. <span data-ttu-id="b9653-174">Wprowadź szczegóły hello w polach hello zgodnie z opisem poniżej-</span><span class="sxs-lookup"><span data-stu-id="b9653-174">Enter hello details in hello fields as described below-</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/Teamphoria_sso_save.png)

    <span data-ttu-id="b9653-176">a.</span><span class="sxs-lookup"><span data-stu-id="b9653-176">a.</span></span> <span data-ttu-id="b9653-177">**Nazwa WYŚWIETLANA** : Wprowadź nazwę wyświetlaną hello wtyczki hello na powitania strony administratora.</span><span class="sxs-lookup"><span data-stu-id="b9653-177">**DISPLAY NAME** : Enter hello display name of hello plugin on hello admin page.</span></span>

    <span data-ttu-id="b9653-178">b.</span><span class="sxs-lookup"><span data-stu-id="b9653-178">b.</span></span> <span data-ttu-id="b9653-179">**Nazwa przycisku** : Nazwa hello hello kartę, która będzie wyświetlana na powitania strony logowania dla logowania za pośrednictwem rejestracji Jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b9653-179">**BUTTON NAME** : hello name of hello tab which will display on hello login page for logging in via SSO.</span></span>

    <span data-ttu-id="b9653-180">c.</span><span class="sxs-lookup"><span data-stu-id="b9653-180">c.</span></span> <span data-ttu-id="b9653-181">**CERTYFIKAT** : Otwórz hello certyfikatu pobrane wcześniej z portalu Azure w programie Notatnik kopiowania zawartości hello hello hello takie same i wklej go w tym miejscu w polu hello.</span><span class="sxs-lookup"><span data-stu-id="b9653-181">**CERTIFICATE** : Open hello Certificate downloaded earlier from hello Azure portal in notepad, copy hello contents of hello same and paste it here in hello box.</span></span>

    <span data-ttu-id="b9653-182">d.</span><span class="sxs-lookup"><span data-stu-id="b9653-182">d.</span></span> <span data-ttu-id="b9653-183">**PUNKT wejścia** : hello Wklej **SAML pojedynczy znak na adres URL usługi** skopiowane wcześniej hello formularza portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="b9653-183">**ENTRY POINT** : Paste hello **SAML Single Sign-On Service URL** copied earlier form hello Azure portal.</span></span>

    <span data-ttu-id="b9653-184">e.</span><span class="sxs-lookup"><span data-stu-id="b9653-184">e.</span></span> <span data-ttu-id="b9653-185">Przełącz opcję hello zbyt**ON** i wybierz polecenie **ZAPISAĆ**.</span><span class="sxs-lookup"><span data-stu-id="b9653-185">Switch hello option too**ON** and click on **SAVE**.</span></span> 

<!--### Next steps

tooensure users can sign-in tooTeamphoria after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Teamphoria prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooTeamphoria in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Teamphoria users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b9653-186">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9653-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="b9653-187">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b9653-187">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="b9653-189">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b9653-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9653-190">W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b9653-190">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b9653-192">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b9653-192">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b9653-194">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b9653-194">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b9653-196">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b9653-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-teamphoria-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b9653-198">a.</span><span class="sxs-lookup"><span data-stu-id="b9653-198">a.</span></span> <span data-ttu-id="b9653-199">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b9653-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9653-200">b.</span><span class="sxs-lookup"><span data-stu-id="b9653-200">b.</span></span> <span data-ttu-id="b9653-201">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b9653-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b9653-202">c.</span><span class="sxs-lookup"><span data-stu-id="b9653-202">c.</span></span> <span data-ttu-id="b9653-203">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="b9653-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b9653-204">d.</span><span class="sxs-lookup"><span data-stu-id="b9653-204">d.</span></span> <span data-ttu-id="b9653-205">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b9653-205">Click **Create**.</span></span>
 
### <a name="creating-a-teamphoria-test-user"></a><span data-ttu-id="b9653-206">Tworzenie użytkownika testowego Teamphoria</span><span class="sxs-lookup"><span data-stu-id="b9653-206">Creating a Teamphoria test user</span></span>

<span data-ttu-id="b9653-207">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Teamphoria muszą mieć przydzielone do Teamphoria.</span><span class="sxs-lookup"><span data-stu-id="b9653-207">In order tooenable Azure AD users toolog into Teamphoria, they must be provisioned into Teamphoria.</span></span> <span data-ttu-id="b9653-208">W przypadku hello Teamphoria Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="b9653-208">In hello case of Teamphoria, provisioning is a manual task.</span></span>

<span data-ttu-id="b9653-209">**tooprovision kont użytkowników, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b9653-209">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9653-210">Zaloguj się za tooyour Teamphoria witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="b9653-210">Log in tooyour Teamphoria company site as an administrator.</span></span>

2. <span data-ttu-id="b9653-211">Polecenie **ADMIN** ustawień na powitania po lewej stronie narzędzi i w obszarze hello **ZARZĄDZAJ** karcie kliknij na **użytkowników** strony administratora hello tooopen dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b9653-211">Click on **ADMIN** settings on hello left toolbar and under hello **MANAGE** tab Click on **USERS** tooopen hello admin page for users.</span></span>

    ![Dodawanie pracownika](./media/active-directory-saas-teamphoria-tutorial/admin_manage_users.png)

3. <span data-ttu-id="b9653-213">Polecenie hello **ZAPROSIĆ RĘCZNEGO** opcji.</span><span class="sxs-lookup"><span data-stu-id="b9653-213">Click on hello **MANUAL INVITE** option.</span></span>

    ![Zaproś inne osoby](./media/active-directory-saas-teamphoria-tutorial/admin_manage_add_users.png)  

4. <span data-ttu-id="b9653-215">Na tej stronie należy wykonać następujące działania.</span><span class="sxs-lookup"><span data-stu-id="b9653-215">On this page, perform following action.</span></span> 
    
    ![Zaproś inne osoby](./media/active-directory-saas-teamphoria-tutorial/manual_user_invite.png)  

    <span data-ttu-id="b9653-217">a.</span><span class="sxs-lookup"><span data-stu-id="b9653-217">a.</span></span> <span data-ttu-id="b9653-218">W hello **adres E-mail** pole tekstowe, hello **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b9653-218">In hello **EMAIL ADDRESS** textbox, hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b9653-219">b.</span><span class="sxs-lookup"><span data-stu-id="b9653-219">b.</span></span> <span data-ttu-id="b9653-220">W hello **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="b9653-220">In hello **FIRST NAME** textbox, type **Britta**.</span></span>

    <span data-ttu-id="b9653-221">c.</span><span class="sxs-lookup"><span data-stu-id="b9653-221">c.</span></span> <span data-ttu-id="b9653-222">W hello **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="b9653-222">In hello **LAST NAME** textbox, type **Simon**.</span></span>

    <span data-ttu-id="b9653-223">d.</span><span class="sxs-lookup"><span data-stu-id="b9653-223">d.</span></span> <span data-ttu-id="b9653-224">Kliknij przycisk **użytkownika zaproszenia 1**.</span><span class="sxs-lookup"><span data-stu-id="b9653-224">Click **INVITE 1 USER**.</span></span> <span data-ttu-id="b9653-225">Użytkownik musi tooget zaproszenia hello tooaccept w systemie hello utworzona.</span><span class="sxs-lookup"><span data-stu-id="b9653-225">User needs tooaccept hello invite tooget created in hello system.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b9653-226">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9653-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b9653-227">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooTeamphoria dostępu.</span><span class="sxs-lookup"><span data-stu-id="b9653-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooTeamphoria.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="b9653-229">**tooassign tooTeamphoria Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b9653-229">**tooassign Britta Simon tooTeamphoria, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9653-230">W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b9653-230">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="b9653-232">Z listy aplikacji hello wybierz **Teamphoria**.</span><span class="sxs-lookup"><span data-stu-id="b9653-232">In hello applications list, select **Teamphoria**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-teamphoria-tutorial/tutorial_teamphoria_app.png) 

3. <span data-ttu-id="b9653-234">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="b9653-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="b9653-236">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b9653-236">Click **Add** button.</span></span> <span data-ttu-id="b9653-237">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b9653-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="b9653-239">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b9653-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b9653-240">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b9653-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b9653-241">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b9653-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b9653-242">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b9653-242">Testing single sign-on</span></span>

<span data-ttu-id="b9653-243">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="b9653-243">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b9653-244">Jeśli chcesz przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="b9653-244">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="b9653-245">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="b9653-245">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b9653-246">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b9653-246">Additional resources</span></span>

* [<span data-ttu-id="b9653-247">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b9653-247">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b9653-248">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b9653-248">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-teamphoria-tutorial/tutorial_general_203.png

