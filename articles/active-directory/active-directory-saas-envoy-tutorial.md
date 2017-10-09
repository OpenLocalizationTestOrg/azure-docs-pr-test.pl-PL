---
title: "Samouczek: Integracji Azure Active Directory z wysłannika | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i wysłannika."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 71f7afcc-1033-4098-9b7e-4f9f2b26f734
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 93add7c1f3cf1fc163acc505f11e34bd696c571c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a><span data-ttu-id="7b16c-103">Samouczek: Integracji Azure Active Directory z wysłannika</span><span class="sxs-lookup"><span data-stu-id="7b16c-103">Tutorial: Azure Active Directory integration with Envoy</span></span>

<span data-ttu-id="7b16c-104">Z tego samouczka, dowiesz się, jak toointegrate wysłannika w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7b16c-104">In this tutorial, you learn how toointegrate Envoy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7b16c-105">Integracja z usługą Azure AD wysłannika zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="7b16c-105">Integrating Envoy with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7b16c-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooEnvoy.</span><span class="sxs-lookup"><span data-stu-id="7b16c-106">You can control in Azure AD who has access tooEnvoy.</span></span>
- <span data-ttu-id="7b16c-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooEnvoy (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b16c-107">You can enable your users tooautomatically get signed-on tooEnvoy (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="7b16c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7b16c-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="7b16c-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7b16c-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b16c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7b16c-110">Prerequisites</span></span>

<span data-ttu-id="7b16c-111">tooconfigure integracji z usługą Azure AD z wysłannika należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="7b16c-111">tooconfigure Azure AD integration with Envoy, you need hello following items:</span></span>

- <span data-ttu-id="7b16c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b16c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7b16c-113">Wysłannika logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7b16c-113">An Envoy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7b16c-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="7b16c-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7b16c-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="7b16c-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7b16c-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="7b16c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7b16c-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7b16c-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7b16c-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="7b16c-118">Scenario description</span></span>
<span data-ttu-id="7b16c-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="7b16c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7b16c-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="7b16c-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7b16c-121">Dodawanie wysłannika z galerii hello</span><span class="sxs-lookup"><span data-stu-id="7b16c-121">Adding Envoy from hello gallery</span></span>
2. <span data-ttu-id="7b16c-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7b16c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-envoy-from-hello-gallery"></a><span data-ttu-id="7b16c-123">Dodawanie wysłannika z galerii hello</span><span class="sxs-lookup"><span data-stu-id="7b16c-123">Adding Envoy from hello gallery</span></span>
<span data-ttu-id="7b16c-124">tooconfigure hello integracja wysłannika programu Azure AD, należy tooadd wysłannika z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="7b16c-124">tooconfigure hello integration of Envoy into Azure AD, you need tooadd Envoy from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7b16c-125">**tooadd wysłannika z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="7b16c-125">**tooadd Envoy from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b16c-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="7b16c-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="7b16c-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="7b16c-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7b16c-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7b16c-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="7b16c-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7b16c-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="7b16c-133">W polu wyszukiwania hello wpisz **wysłannika**, wybierz pozycję **wysłannika** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="7b16c-133">In hello search box, type **Envoy**, select **Envoy** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Wysłannika hello listy wyników](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7b16c-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7b16c-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7b16c-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z wysłannika w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="7b16c-136">In this section, you configure and test Azure AD single sign-on with Envoy based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7b16c-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w wysłannika jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7b16c-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Envoy is tooa user in Azure AD.</span></span> <span data-ttu-id="7b16c-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w wysłannika musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="7b16c-138">In other words, a link relationship between an Azure AD user and hello related user in Envoy needs toobe established.</span></span>

<span data-ttu-id="7b16c-139">W wysłannika, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="7b16c-139">In Envoy, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7b16c-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z wysłannika, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="7b16c-140">tooconfigure and test Azure AD single sign-on with Envoy, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7b16c-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="7b16c-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7b16c-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7b16c-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7b16c-143">**[Tworzenie użytkownika testowego wysłannika](#create-an-envoy-test-user)**  -toohave odpowiednikiem Simona Britta w wysłannika, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7b16c-143">**[Create an Envoy test user](#create-an-envoy-test-user)** - toohave a counterpart of Britta Simon in Envoy that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7b16c-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="7b16c-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7b16c-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="7b16c-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7b16c-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7b16c-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7b16c-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji wysłannika.</span><span class="sxs-lookup"><span data-stu-id="7b16c-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Envoy application.</span></span>

<span data-ttu-id="7b16c-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z wysłannika, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="7b16c-148">**tooconfigure Azure AD single sign-on with Envoy, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b16c-149">W portalu Azure na powitania hello **wysłannika** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="7b16c-149">In hello Azure portal, on hello **Envoy** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="7b16c-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="7b16c-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_samlbase.png)

3. <span data-ttu-id="7b16c-153">Na powitania **wysłannika domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="7b16c-153">On hello **Envoy Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i domeny wysłannika pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_url.png)

    <span data-ttu-id="7b16c-155">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<tenant-name>.Envoy.com`</span><span class="sxs-lookup"><span data-stu-id="7b16c-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Envoy.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="7b16c-156">Ta wartość nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="7b16c-156">This value is not real.</span></span> <span data-ttu-id="7b16c-157">Zaktualizuj tę wartość z hello rzeczywisty adres URL logowania.</span><span class="sxs-lookup"><span data-stu-id="7b16c-157">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="7b16c-158">Skontaktuj się z [zespołem pomocy technicznej klienta wysłannika](https://envoy.com/contact/) tooget tej wartości.</span><span class="sxs-lookup"><span data-stu-id="7b16c-158">Contact [Envoy Client support team](https://envoy.com/contact/) tooget this value.</span></span>

4. <span data-ttu-id="7b16c-159">Na powitania **certyfikat podpisywania SAML** hello kopiowania, sekcji **odcisk PALCA** wartość certyfikat...</span><span class="sxs-lookup"><span data-stu-id="7b16c-159">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate..</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_certificate.png) 

5. <span data-ttu-id="7b16c-161">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7b16c-161">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-envoy-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7b16c-163">Na powitania **konfiguracji wysłannika** kliknij **skonfigurować wysłannika** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="7b16c-163">On hello **Envoy Configuration** section, click **Configure Envoy** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7b16c-164">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="7b16c-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfiguracja wysłannika](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_configure.png)

7. <span data-ttu-id="7b16c-166">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy wysłannika jako administrator.</span><span class="sxs-lookup"><span data-stu-id="7b16c-166">In a different web browser window, log into your Envoy company site as an administrator.</span></span>

8. <span data-ttu-id="7b16c-167">Witaj pasku narzędzi u góry hello, kliknij przycisk **ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="7b16c-167">In hello toolbar on hello top, click **Settings**.</span></span>

    <span data-ttu-id="7b16c-168">![Wysłannika](./media/active-directory-saas-envoy-tutorial/ic776782.png "wysłannika")</span><span class="sxs-lookup"><span data-stu-id="7b16c-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span></span>

9. <span data-ttu-id="7b16c-169">Kliknij przycisk **firmy**.</span><span class="sxs-lookup"><span data-stu-id="7b16c-169">Click **Company**.</span></span>

    <span data-ttu-id="7b16c-170">![Firmy](./media/active-directory-saas-envoy-tutorial/ic776783.png "firmy")</span><span class="sxs-lookup"><span data-stu-id="7b16c-170">![Company](./media/active-directory-saas-envoy-tutorial/ic776783.png "Company")</span></span>

10. <span data-ttu-id="7b16c-171">Kliknij przycisk **SAML**.</span><span class="sxs-lookup"><span data-stu-id="7b16c-171">Click **SAML**.</span></span>

    <span data-ttu-id="7b16c-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="7b16c-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span></span>

11. <span data-ttu-id="7b16c-173">W hello **uwierzytelnianie SAML** konfiguracji sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="7b16c-173">In hello **SAML Authentication** configuration section, perform hello following steps:</span></span>

    <span data-ttu-id="7b16c-174">![Uwierzytelnianie SAML](./media/active-directory-saas-envoy-tutorial/ic776785.png "uwierzytelnianie SAML")</span><span class="sxs-lookup"><span data-stu-id="7b16c-174">![SAML authentication](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML authentication")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="7b16c-175">wartość Hello identyfikator lokalizacji HQ hello jest automatycznie generowane przez aplikację hello.</span><span class="sxs-lookup"><span data-stu-id="7b16c-175">hello value for hello HQ location ID is auto generated by hello application.</span></span>
    
    <span data-ttu-id="7b16c-176">a.</span><span class="sxs-lookup"><span data-stu-id="7b16c-176">a.</span></span> <span data-ttu-id="7b16c-177">W **odcisk palca** pole tekstowe, Wklej hello **odcisk palca** wartość certyfikatów, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7b16c-177">In **Fingerprint** textbox, paste hello **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="7b16c-178">b.</span><span class="sxs-lookup"><span data-stu-id="7b16c-178">b.</span></span> <span data-ttu-id="7b16c-179">Wklej **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana tworzą hello Azure portalu do hello **URL SAML HTTP dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="7b16c-179">Paste **SAML Single Sign-On Service URL** value, which you have copied form hello Azure portal into hello **IDENTITY PROVIDER HTTP SAML URL** textbox.</span></span>
    
    <span data-ttu-id="7b16c-180">c.</span><span class="sxs-lookup"><span data-stu-id="7b16c-180">c.</span></span> <span data-ttu-id="7b16c-181">Kliknij przycisk **zapisać zmiany**.</span><span class="sxs-lookup"><span data-stu-id="7b16c-181">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="7b16c-182">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="7b16c-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7b16c-183">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="7b16c-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7b16c-184">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7b16c-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7b16c-185">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b16c-185">Create an Azure AD test user</span></span>

<span data-ttu-id="7b16c-186">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="7b16c-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="7b16c-188">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="7b16c-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b16c-189">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7b16c-189">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-envoy-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="7b16c-191">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="7b16c-191">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-envoy-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="7b16c-193">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="7b16c-193">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-envoy-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="7b16c-195">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7b16c-195">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-envoy-tutorial/create_aaduser_04.png)

    <span data-ttu-id="7b16c-197">a.</span><span class="sxs-lookup"><span data-stu-id="7b16c-197">a.</span></span> <span data-ttu-id="7b16c-198">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7b16c-198">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7b16c-199">b.</span><span class="sxs-lookup"><span data-stu-id="7b16c-199">b.</span></span> <span data-ttu-id="7b16c-200">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7b16c-200">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="7b16c-201">c.</span><span class="sxs-lookup"><span data-stu-id="7b16c-201">c.</span></span> <span data-ttu-id="7b16c-202">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="7b16c-202">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="7b16c-203">d.</span><span class="sxs-lookup"><span data-stu-id="7b16c-203">d.</span></span> <span data-ttu-id="7b16c-204">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7b16c-204">Click **Create**.</span></span>
 
### <a name="create-an-envoy-test-user"></a><span data-ttu-id="7b16c-205">Tworzenie użytkownika testowego wysłannika</span><span class="sxs-lookup"><span data-stu-id="7b16c-205">Create an Envoy test user</span></span>

<span data-ttu-id="7b16c-206">Nie ma elementu akcji można tooconfigure użytkownika inicjowania obsługi administracyjnej tooEnvoy.</span><span class="sxs-lookup"><span data-stu-id="7b16c-206">There is no action item for you tooconfigure user provisioning tooEnvoy.</span></span> <span data-ttu-id="7b16c-207">Gdy przypisany użytkownik podejmie próbę toolog do wysłannika za pomocą panelu dostępu hello, wysłannika sprawdza, czy istnieje hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7b16c-207">When an assigned user tries toolog into Envoy using hello access panel, Envoy checks whether hello user exists.</span></span> <span data-ttu-id="7b16c-208">Jeśli nie jest Brak konta użytkownika dostępny jeszcze, są tworzone przez wysłannika.</span><span class="sxs-lookup"><span data-stu-id="7b16c-208">If there is no user account available yet, it is automatically created by Envoy.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7b16c-209">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7b16c-209">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7b16c-210">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooEnvoy.</span><span class="sxs-lookup"><span data-stu-id="7b16c-210">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEnvoy.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="7b16c-212">**tooassign tooEnvoy Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="7b16c-212">**tooassign Britta Simon tooEnvoy, perform hello following steps:**</span></span>

1. <span data-ttu-id="7b16c-213">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7b16c-213">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="7b16c-215">Z listy aplikacji hello wybierz **wysłannika**.</span><span class="sxs-lookup"><span data-stu-id="7b16c-215">In hello applications list, select **Envoy**.</span></span>

    ![łącze wysłannika Hello na liście aplikacji hello](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_app.png)  

3. <span data-ttu-id="7b16c-217">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="7b16c-217">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="7b16c-219">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7b16c-219">Click **Add** button.</span></span> <span data-ttu-id="7b16c-220">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7b16c-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="7b16c-222">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="7b16c-222">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7b16c-223">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7b16c-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7b16c-224">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7b16c-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7b16c-225">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7b16c-225">Test single sign-on</span></span>

<span data-ttu-id="7b16c-226">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="7b16c-226">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7b16c-227">Po kliknięciu kafelka wysłannika hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour wysłannika aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7b16c-227">When you click hello Envoy tile in hello Access Panel, you should get automatically signed-on tooyour Envoy application.</span></span>
<span data-ttu-id="7b16c-228">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7b16c-228">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7b16c-229">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="7b16c-229">Additional resources</span></span>

* [<span data-ttu-id="7b16c-230">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7b16c-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7b16c-231">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7b16c-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_203.png

