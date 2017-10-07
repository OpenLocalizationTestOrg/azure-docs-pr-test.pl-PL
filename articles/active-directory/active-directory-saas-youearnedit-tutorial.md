---
title: 'Samouczek: Integracji Azure Active Directory z YouEarnedIt | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i YouEarnedIt."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 3011d44d-dfcf-4061-888f-cff90fbc8150
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: jeedes
ms.openlocfilehash: cc9a8ae2f92751cf3fadbeec23c8319c83728a33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-youearnedit"></a><span data-ttu-id="71ab1-103">Samouczek: Integracji Azure Active Directory z YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="71ab1-103">Tutorial: Azure Active Directory integration with YouEarnedIt</span></span>

<span data-ttu-id="71ab1-104">Z tego samouczka, dowiesz się, jak toointegrate YouEarnedIt w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="71ab1-104">In this tutorial, you learn how toointegrate YouEarnedIt with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="71ab1-105">Integracja z usługą Azure AD YouEarnedIt zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="71ab1-105">Integrating YouEarnedIt with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="71ab1-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooYouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="71ab1-106">You can control in Azure AD who has access tooYouEarnedIt.</span></span>
- <span data-ttu-id="71ab1-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooYouEarnedIt (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71ab1-107">You can enable your users tooautomatically get signed-on tooYouEarnedIt (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="71ab1-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="71ab1-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="71ab1-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="71ab1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71ab1-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="71ab1-110">Prerequisites</span></span>

<span data-ttu-id="71ab1-111">tooconfigure integracji z usługą Azure AD z YouEarnedIt należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="71ab1-111">tooconfigure Azure AD integration with YouEarnedIt, you need hello following items:</span></span>

- <span data-ttu-id="71ab1-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="71ab1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="71ab1-113">YouEarnedIt logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="71ab1-113">A YouEarnedIt single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="71ab1-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="71ab1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="71ab1-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="71ab1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="71ab1-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="71ab1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="71ab1-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="71ab1-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="71ab1-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="71ab1-118">Scenario description</span></span>
<span data-ttu-id="71ab1-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="71ab1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="71ab1-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="71ab1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="71ab1-121">Dodawanie YouEarnedIt z galerii hello</span><span class="sxs-lookup"><span data-stu-id="71ab1-121">Adding YouEarnedIt from hello gallery</span></span>
2. <span data-ttu-id="71ab1-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="71ab1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-youearnedit-from-hello-gallery"></a><span data-ttu-id="71ab1-123">Dodawanie YouEarnedIt z galerii hello</span><span class="sxs-lookup"><span data-stu-id="71ab1-123">Adding YouEarnedIt from hello gallery</span></span>
<span data-ttu-id="71ab1-124">tooconfigure hello integracji YouEarnedIt do usługi Azure AD, należy tooadd YouEarnedIt z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="71ab1-124">tooconfigure hello integration of YouEarnedIt into Azure AD, you need tooadd YouEarnedIt from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="71ab1-125">**tooadd YouEarnedIt z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="71ab1-125">**tooadd YouEarnedIt from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="71ab1-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="71ab1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="71ab1-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="71ab1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="71ab1-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="71ab1-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="71ab1-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="71ab1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="71ab1-133">W polu wyszukiwania hello wpisz **YouEarnedt**, wybierz pozycję **YouEarnedt** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="71ab1-133">In hello search box, type **YouEarnedt**, select  **YouEarnedt**  from result panel then click **Add** button tooadd hello application.</span></span>

    ![YouEarnedIt hello listy wyników](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="71ab1-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="71ab1-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="71ab1-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z YouEarnedIt w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="71ab1-136">In this section, you configure and test Azure AD single sign-on with YouEarnedIt based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="71ab1-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w YouEarnedIt jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="71ab1-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in YouEarnedIt is tooa user in Azure AD.</span></span> <span data-ttu-id="71ab1-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w YouEarnedIt musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="71ab1-138">In other words, a link relationship between an Azure AD user and hello related user in YouEarnedIt needs toobe established.</span></span>

<span data-ttu-id="71ab1-139">W YouEarnedIt, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="71ab1-139">In YouEarnedIt, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="71ab1-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z YouEarnedIt, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="71ab1-140">tooconfigure and test Azure AD single sign-on with YouEarnedIt, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="71ab1-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="71ab1-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="71ab1-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="71ab1-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="71ab1-143">**[Tworzenie użytkownika testowego YouEarnedIt](#create-a-youearnedit-test-user)**  -toohave odpowiednikiem Simona Britta w YouEarnedIt, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="71ab1-143">**[Create a YouEarnedIt test user](#create-a-youearnedit-test-user)** - toohave a counterpart of Britta Simon in YouEarnedIt that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="71ab1-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="71ab1-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="71ab1-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="71ab1-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="71ab1-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="71ab1-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="71ab1-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="71ab1-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your YouEarnedIt application.</span></span>

<span data-ttu-id="71ab1-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z YouEarnedIt, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="71ab1-148">**tooconfigure Azure AD single sign-on with YouEarnedIt, perform hello following steps:**</span></span>

1. <span data-ttu-id="71ab1-149">W portalu Azure na powitania hello **YouEarnedIt** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="71ab1-149">In hello Azure portal, on hello **YouEarnedIt** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="71ab1-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="71ab1-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_samlbase.png)

3. <span data-ttu-id="71ab1-153">Na powitania **YouEarnedIt domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="71ab1-153">On hello **YouEarnedIt Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i domeny YouEarnedIt pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_url.png)

    <span data-ttu-id="71ab1-155">a.</span><span class="sxs-lookup"><span data-stu-id="71ab1-155">a.</span></span> <span data-ttu-id="71ab1-156">W hello **adres URL logowania** tekstowym, wpisz adres URL przy użyciu następującego hello wzorców:</span><span class="sxs-lookup"><span data-stu-id="71ab1-156">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
    | <span data-ttu-id="71ab1-157">Środowisko</span><span class="sxs-lookup"><span data-stu-id="71ab1-157">Environment</span></span>  | <span data-ttu-id="71ab1-158">wzorzec</span><span class="sxs-lookup"><span data-stu-id="71ab1-158">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="71ab1-159">Produkcji</span><span class="sxs-lookup"><span data-stu-id="71ab1-159">Production</span></span> | `https://<company name>.youearnedit.com/users/sign_in` |
    | <span data-ttu-id="71ab1-160">Piaskownica</span><span class="sxs-lookup"><span data-stu-id="71ab1-160">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com/users/sign_in` |

    <span data-ttu-id="71ab1-161">b.</span><span class="sxs-lookup"><span data-stu-id="71ab1-161">b.</span></span> <span data-ttu-id="71ab1-162">W hello **identyfikator** tekstowym, wpisz adres URL przy użyciu następującego hello wzorców:</span><span class="sxs-lookup"><span data-stu-id="71ab1-162">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span>
    | <span data-ttu-id="71ab1-163">Środowisko</span><span class="sxs-lookup"><span data-stu-id="71ab1-163">Environment</span></span>  | <span data-ttu-id="71ab1-164">wzorzec</span><span class="sxs-lookup"><span data-stu-id="71ab1-164">Pattern</span></span>  |
    |:--- |:--- |
    | <span data-ttu-id="71ab1-165">Produkcji</span><span class="sxs-lookup"><span data-stu-id="71ab1-165">Production</span></span> | `https://<company name>.youearnedit.com` |
    | <span data-ttu-id="71ab1-166">Piaskownica</span><span class="sxs-lookup"><span data-stu-id="71ab1-166">Sandbox</span></span>  |`https://<company name>.sandbox.youearnedit.com` |

    > [!NOTE] 
    > <span data-ttu-id="71ab1-167">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="71ab1-167">These values are not real.</span></span> <span data-ttu-id="71ab1-168">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="71ab1-168">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="71ab1-169">Skontaktuj się z [zespołem pomocy technicznej klienta YouEarnedIt](https://youearnedit.freshdesk.com/support/tickets/new) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="71ab1-169">Contact [YouEarnedIt Client support team](https://youearnedit.freshdesk.com/support/tickets/new) tooget these values.</span></span> 
 
4. <span data-ttu-id="71ab1-170">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="71ab1-170">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_certificate.png) 

5. <span data-ttu-id="71ab1-172">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="71ab1-172">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-youearnedit-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="71ab1-174">Na powitania **konfiguracji YouEarnedIt** kliknij **skonfigurować YouEarnedIt** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="71ab1-174">On hello **YouEarnedIt Configuration** section, click **Configure YouEarnedIt** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="71ab1-175">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="71ab1-175">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfiguracja YouEarnedIt](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_configure.png) 

7. <span data-ttu-id="71ab1-177">tooconfigure rejestracji jednokrotnej w **YouEarnedIt** strony, należy pobrać hello toosend **Certificate(Base64)** i **SAML pojedynczy znak na adres URL usługi** za[Zespołem pomocy technicznej YouEarnedIt](https://youearnedit.freshdesk.com/support/tickets/new).</span><span class="sxs-lookup"><span data-stu-id="71ab1-177">tooconfigure single sign-on on **YouEarnedIt** side, you need toosend hello downloaded **Certificate(Base64)** and **SAML Single Sign-On Service URL** too[YouEarnedIt support team](https://youearnedit.freshdesk.com/support/tickets/new).</span></span> <span data-ttu-id="71ab1-178">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="71ab1-178">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="71ab1-179">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="71ab1-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="71ab1-180">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="71ab1-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="71ab1-181">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="71ab1-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="71ab1-182">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="71ab1-182">Create an Azure AD test user</span></span>

<span data-ttu-id="71ab1-183">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="71ab1-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="71ab1-185">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="71ab1-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="71ab1-186">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="71ab1-186">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="71ab1-188">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="71ab1-188">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="71ab1-190">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="71ab1-190">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="71ab1-192">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="71ab1-192">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-youearnedit-tutorial/create_aaduser_04.png)

    <span data-ttu-id="71ab1-194">a.</span><span class="sxs-lookup"><span data-stu-id="71ab1-194">a.</span></span> <span data-ttu-id="71ab1-195">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="71ab1-195">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="71ab1-196">b.</span><span class="sxs-lookup"><span data-stu-id="71ab1-196">b.</span></span> <span data-ttu-id="71ab1-197">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="71ab1-197">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="71ab1-198">c.</span><span class="sxs-lookup"><span data-stu-id="71ab1-198">c.</span></span> <span data-ttu-id="71ab1-199">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="71ab1-199">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="71ab1-200">d.</span><span class="sxs-lookup"><span data-stu-id="71ab1-200">d.</span></span> <span data-ttu-id="71ab1-201">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="71ab1-201">Click **Create**.</span></span>
 
### <a name="create-a-youearnedit-test-user"></a><span data-ttu-id="71ab1-202">Tworzenie użytkownika testowego YouEarnedIt</span><span class="sxs-lookup"><span data-stu-id="71ab1-202">Create a YouEarnedIt test user</span></span>

<span data-ttu-id="71ab1-203">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w YouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="71ab1-203">In this section, you create a user called Britta Simon in YouEarnedIt.</span></span> <span data-ttu-id="71ab1-204">Należy skontaktować się z użytkowników zespołu pomocy technicznej YouEarnedIt hello tooadd hello YouEarnedIt platformy.</span><span class="sxs-lookup"><span data-stu-id="71ab1-204">Please work with YouEarnedIt support team tooadd hello users in hello YouEarnedIt platform.</span></span>

>[!NOTE]
><span data-ttu-id="71ab1-205">YouEarnedIt oczekiwać hello dostawcy tożsamości toosupply EmailAddress lub nazwy użytkownika w atrybucie NameID hello.</span><span class="sxs-lookup"><span data-stu-id="71ab1-205">YouEarnedIt expect hello Identity Provider toosupply an EmailAddress  or UserName in hello NameID attribute.</span></span> <span data-ttu-id="71ab1-206">Uwierzytelnianie nie powiedzie się, jeśli odpowiednie nazwy użytkownika i EmailAddress nie został znaleziony w bazie danych hello lub nie jest dokładnie zgodny.</span><span class="sxs-lookup"><span data-stu-id="71ab1-206">Authentication will fail if a corresponding UserName or EmailAddress is not found within hello database or does not match exactly.</span></span> <span data-ttu-id="71ab1-207">Będzie to wymagało, że konta będzie importowana do systemu YouEarnedIt hello przed hello integracji logowania jednokrotnego, (zazwyczaj albo za pośrednictwem interfejsu API lub CSV import).</span><span class="sxs-lookup"><span data-stu-id="71ab1-207">This will require that accounts be imported into hello YouEarnedIt system before hello SSO integration (Typically either via API or CSV import).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="71ab1-208">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="71ab1-208">Assign hello Azure AD test user</span></span>

<span data-ttu-id="71ab1-209">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooYouEarnedIt.</span><span class="sxs-lookup"><span data-stu-id="71ab1-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooYouEarnedIt.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="71ab1-211">**tooassign tooYouEarnedIt Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="71ab1-211">**tooassign Britta Simon tooYouEarnedIt, perform hello following steps:**</span></span>

1. <span data-ttu-id="71ab1-212">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="71ab1-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="71ab1-214">Z listy aplikacji hello wybierz **YouEarnedIt**.</span><span class="sxs-lookup"><span data-stu-id="71ab1-214">In hello applications list, select **YouEarnedIt**.</span></span>

    ![łącze YouEarnedIt Hello na liście aplikacji hello](./media/active-directory-saas-youearnedit-tutorial/tutorial_youearnedit_app.png)  

3. <span data-ttu-id="71ab1-216">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="71ab1-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="71ab1-218">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="71ab1-218">Click **Add** button.</span></span> <span data-ttu-id="71ab1-219">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="71ab1-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="71ab1-221">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="71ab1-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="71ab1-222">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="71ab1-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="71ab1-223">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="71ab1-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="71ab1-224">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="71ab1-224">Test single sign-on</span></span>

<span data-ttu-id="71ab1-225">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="71ab1-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="71ab1-226">Po kliknięciu kafelka YouEarnedIt hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour YouEarnedIt aplikacji.</span><span class="sxs-lookup"><span data-stu-id="71ab1-226">When you click hello YouEarnedIt tile in hello Access Panel, you should get automatically signed-on tooyour YouEarnedIt application.</span></span>
<span data-ttu-id="71ab1-227">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="71ab1-227">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="71ab1-228">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="71ab1-228">Additional resources</span></span>

* [<span data-ttu-id="71ab1-229">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="71ab1-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="71ab1-230">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="71ab1-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-youearnedit-tutorial/tutorial_general_203.png

