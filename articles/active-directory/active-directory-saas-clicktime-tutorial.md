---
title: 'Samouczek: Integracji Azure Active Directory z ClickTime | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i ClickTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: a0259e31164cad6c6c77ed8aac1c50cd9a3e46ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a><span data-ttu-id="7e04a-103">Samouczek: Integracji Azure Active Directory z ClickTime</span><span class="sxs-lookup"><span data-stu-id="7e04a-103">Tutorial: Azure Active Directory integration with ClickTime</span></span>

<span data-ttu-id="7e04a-104">Z tego samouczka, dowiesz się, jak toointegrate ClickTime w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7e04a-104">In this tutorial, you learn how toointegrate ClickTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7e04a-105">Integracja z usługą Azure AD ClickTime zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="7e04a-105">Integrating ClickTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="7e04a-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooClickTime</span><span class="sxs-lookup"><span data-stu-id="7e04a-106">You can control in Azure AD who has access tooClickTime</span></span>
- <span data-ttu-id="7e04a-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooClickTime (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e04a-107">You can enable your users tooautomatically get signed-on tooClickTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7e04a-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="7e04a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="7e04a-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7e04a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e04a-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7e04a-110">Prerequisites</span></span>

<span data-ttu-id="7e04a-111">tooconfigure integracji z usługą Azure AD z ClickTime należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="7e04a-111">tooconfigure Azure AD integration with ClickTime, you need hello following items:</span></span>

- <span data-ttu-id="7e04a-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e04a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7e04a-113">ClickTime logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7e04a-113">A ClickTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7e04a-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="7e04a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7e04a-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="7e04a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7e04a-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="7e04a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7e04a-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7e04a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7e04a-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="7e04a-118">Scenario description</span></span>
<span data-ttu-id="7e04a-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="7e04a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7e04a-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="7e04a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7e04a-121">Dodawanie ClickTime z galerii hello</span><span class="sxs-lookup"><span data-stu-id="7e04a-121">Adding ClickTime from hello gallery</span></span>
2. <span data-ttu-id="7e04a-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7e04a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clicktime-from-hello-gallery"></a><span data-ttu-id="7e04a-123">Dodawanie ClickTime z galerii hello</span><span class="sxs-lookup"><span data-stu-id="7e04a-123">Adding ClickTime from hello gallery</span></span>
<span data-ttu-id="7e04a-124">tooconfigure hello integracji ClickTime do usługi Azure AD, należy tooadd ClickTime z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="7e04a-124">tooconfigure hello integration of ClickTime into Azure AD, you need tooadd ClickTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="7e04a-125">**tooadd ClickTime z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="7e04a-125">**tooadd ClickTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e04a-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="7e04a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="7e04a-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="7e04a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="7e04a-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7e04a-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="7e04a-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7e04a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="7e04a-133">W polu wyszukiwania hello wpisz **ClickTime**, wybierz pozycję **ClickTime** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="7e04a-133">In hello search box, type **ClickTime**, select **ClickTime** from result panel then click **Add** button tooadd hello application.</span></span>

    ![ClickTime hello listy wyników](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="7e04a-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7e04a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="7e04a-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z ClickTime w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="7e04a-136">In this section, you configure and test Azure AD single sign-on with ClickTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7e04a-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w ClickTime jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e04a-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ClickTime is tooa user in Azure AD.</span></span> <span data-ttu-id="7e04a-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w ClickTime musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="7e04a-138">In other words, a link relationship between an Azure AD user and hello related user in ClickTime needs toobe established.</span></span>

<span data-ttu-id="7e04a-139">W ClickTime, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="7e04a-139">In ClickTime, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="7e04a-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z ClickTime, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="7e04a-140">tooconfigure and test Azure AD single sign-on with ClickTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="7e04a-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="7e04a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="7e04a-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7e04a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7e04a-143">**[Tworzenie użytkownika testowego ClickTime](#create-a-clicktime-test-user)**  -toohave odpowiednikiem Simona Britta w ClickTime, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="7e04a-143">**[Create a ClickTime test user](#create-a-clicktime-test-user)** - toohave a counterpart of Britta Simon in ClickTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="7e04a-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="7e04a-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7e04a-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="7e04a-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="7e04a-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7e04a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="7e04a-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji ClickTime.</span><span class="sxs-lookup"><span data-stu-id="7e04a-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ClickTime application.</span></span>

<span data-ttu-id="7e04a-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z ClickTime, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="7e04a-148">**tooconfigure Azure AD single sign-on with ClickTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e04a-149">W portalu Azure na powitania hello **ClickTime** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="7e04a-149">In hello Azure portal, on hello **ClickTime** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="7e04a-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="7e04a-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. <span data-ttu-id="7e04a-153">Na powitania **ClickTime domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="7e04a-153">On hello **ClickTime Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i domeny ClickTime pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    <span data-ttu-id="7e04a-155">a.</span><span class="sxs-lookup"><span data-stu-id="7e04a-155">a.</span></span> <span data-ttu-id="7e04a-156">W hello **identyfikator** tekstowym, wpisz adres URL jako:`https://app.clicktime.com/sp/`</span><span class="sxs-lookup"><span data-stu-id="7e04a-156">In hello **Identifier** textbox, type a URL as: `https://app.clicktime.com/sp/`</span></span>
    
    <span data-ttu-id="7e04a-157">b.</span><span class="sxs-lookup"><span data-stu-id="7e04a-157">b.</span></span> <span data-ttu-id="7e04a-158">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL przy użyciu następującego hello wzorców:</span><span class="sxs-lookup"><span data-stu-id="7e04a-158">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. <span data-ttu-id="7e04a-159">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="7e04a-159">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. <span data-ttu-id="7e04a-161">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7e04a-161">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7e04a-163">Na powitania **konfiguracji ClickTime** kliknij **skonfigurować ClickTime** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="7e04a-163">On hello **ClickTime Configuration** section, click **Configure ClickTime** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="7e04a-164">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="7e04a-164">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfiguracja ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. <span data-ttu-id="7e04a-166">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy ClickTime jako administrator.</span><span class="sxs-lookup"><span data-stu-id="7e04a-166">In a different web browser window, log into your ClickTime company site as an administrator.</span></span>

8. <span data-ttu-id="7e04a-167">Witaj pasku narzędzi u góry hello, kliknij przycisk **preferencje**, a następnie kliknij przycisk **ustawienia zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="7e04a-167">In hello toolbar on hello top, click **Preferences**, and then click **Security Settings**.</span></span>

9. <span data-ttu-id="7e04a-168">W hello **preferencje rejestracji jednokrotnej** konfiguracji sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="7e04a-168">In hello **Single Sign-On Preferences** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="7e04a-169">![Ustawienia zabezpieczeń](./media/active-directory-saas-clicktime-tutorial/tic777280.png "ustawienia zabezpieczeń")</span><span class="sxs-lookup"><span data-stu-id="7e04a-169">![Security Settings](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Security Settings")</span></span>
   
    <span data-ttu-id="7e04a-170">a.</span><span class="sxs-lookup"><span data-stu-id="7e04a-170">a.</span></span>  <span data-ttu-id="7e04a-171">Wybierz **Zezwalaj** Zaloguj się przy użyciu pojedynczego logowania jednokrotnego (SSO) z **usługi Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="7e04a-171">Select **Allow** sign-in using Single Sign-On (SSO) with **Azure AD**.</span></span>
   
    <span data-ttu-id="7e04a-172">b.</span><span class="sxs-lookup"><span data-stu-id="7e04a-172">b.</span></span> <span data-ttu-id="7e04a-173">W hello **punktu końcowego dostawcy tożsamości** pole tekstowe, Wklej **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="7e04a-173">In hello **Identity Provider Endpoint** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="7e04a-174">c.</span><span class="sxs-lookup"><span data-stu-id="7e04a-174">c.</span></span>  <span data-ttu-id="7e04a-175">Otwórz hello **certyfikatu algorytmem base-64** pobrany z portalu Azure w **Notatnik**, skopiuj zawartość hello i wkleić go do hello **certyfikatu X.509** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="7e04a-175">Open hello **base-64 encoded certificate** downloaded from Azure portal in **Notepad**, copy hello content, and then paste it into hello **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="7e04a-176">d.</span><span class="sxs-lookup"><span data-stu-id="7e04a-176">d.</span></span>  <span data-ttu-id="7e04a-177">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="7e04a-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="7e04a-178">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="7e04a-178">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="7e04a-179">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="7e04a-179">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="7e04a-180">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="7e04a-180">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="7e04a-181">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e04a-181">Create an Azure AD test user</span></span>
<span data-ttu-id="7e04a-182">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="7e04a-182">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="7e04a-184">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="7e04a-184">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e04a-185">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7e04a-185">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7e04a-187">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="7e04a-187">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>
    
    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7e04a-189">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="7e04a-189">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>
 
    ![przycisk Dodaj Hello](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7e04a-191">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7e04a-191">In hello **User** dialog box, perform hello following steps:</span></span>
 
    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7e04a-193">a.</span><span class="sxs-lookup"><span data-stu-id="7e04a-193">a.</span></span> <span data-ttu-id="7e04a-194">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7e04a-194">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7e04a-195">b.</span><span class="sxs-lookup"><span data-stu-id="7e04a-195">b.</span></span> <span data-ttu-id="7e04a-196">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7e04a-196">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7e04a-197">c.</span><span class="sxs-lookup"><span data-stu-id="7e04a-197">c.</span></span> <span data-ttu-id="7e04a-198">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="7e04a-198">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="7e04a-199">d.</span><span class="sxs-lookup"><span data-stu-id="7e04a-199">d.</span></span> <span data-ttu-id="7e04a-200">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="7e04a-200">Click **Create**.</span></span>
 
### <a name="create-a-clicktime-test-user"></a><span data-ttu-id="7e04a-201">Tworzenie użytkownika testowego ClickTime</span><span class="sxs-lookup"><span data-stu-id="7e04a-201">Create a ClickTime test user</span></span>

<span data-ttu-id="7e04a-202">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do ClickTime muszą mieć przydzielone do ClickTime.</span><span class="sxs-lookup"><span data-stu-id="7e04a-202">In order tooenable Azure AD users toolog into ClickTime, they must be provisioned into ClickTime.</span></span>  
<span data-ttu-id="7e04a-203">W przypadku hello ClickTime Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="7e04a-203">In hello case of ClickTime, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="7e04a-204">Możesz użyć innych ClickTime użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez ClickTime tooprovision kont użytkowników usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7e04a-204">You can use any other ClickTime user account creation tools or APIs provided by ClickTime tooprovision Azure AD user accounts.</span></span>

<span data-ttu-id="7e04a-205">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="7e04a-205">**tooprovision a user account, perform hello following steps:**</span></span>
1. <span data-ttu-id="7e04a-206">Zaloguj się za tooyour **ClickTime** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="7e04a-206">Log in tooyour **ClickTime** tenant.</span></span>
2. <span data-ttu-id="7e04a-207">Witaj pasku narzędzi u góry hello, kliknij przycisk **firmy**, a następnie kliknij przycisk **osób**.</span><span class="sxs-lookup"><span data-stu-id="7e04a-207">In hello toolbar on hello top, click **Company**, and then click **People**.</span></span>
   
    <span data-ttu-id="7e04a-208">![Osoby](./media/active-directory-saas-clicktime-tutorial/tic777282.png "osób")</span><span class="sxs-lookup"><span data-stu-id="7e04a-208">![People](./media/active-directory-saas-clicktime-tutorial/tic777282.png "People")</span></span>
3. <span data-ttu-id="7e04a-209">Kliknij przycisk **Dodaj osobę**.</span><span class="sxs-lookup"><span data-stu-id="7e04a-209">Click **Add Person**.</span></span>
   
    <span data-ttu-id="7e04a-210">![Dodaj osobę](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Dodaj osobę")</span><span class="sxs-lookup"><span data-stu-id="7e04a-210">![Add Person](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Add Person")</span></span>
4. <span data-ttu-id="7e04a-211">W sekcji nowej osoby hello wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="7e04a-211">In hello New Person section, perform hello following steps:</span></span>
   
    <span data-ttu-id="7e04a-212">![Osoby](./media/active-directory-saas-clicktime-tutorial/tic777284.png "osób")</span><span class="sxs-lookup"><span data-stu-id="7e04a-212">![People](./media/active-directory-saas-clicktime-tutorial/tic777284.png "People")</span></span>
   
    <span data-ttu-id="7e04a-213">a.</span><span class="sxs-lookup"><span data-stu-id="7e04a-213">a.</span></span>  <span data-ttu-id="7e04a-214">W hello **Pełna nazwa** pole tekstowe, typ Pełna nazwa użytkownika, takich jak **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="7e04a-214">In hello **full name** textbox, type full name of user like **Britta Simon**.</span></span> 
  
    <span data-ttu-id="7e04a-215">b.</span><span class="sxs-lookup"><span data-stu-id="7e04a-215">b.</span></span>  <span data-ttu-id="7e04a-216">W hello **adres e-mail** pole tekstowe, powitalne wiadomości e-mail użytkownika, takich jak  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="7e04a-216">In hello **email address** textbox, type hello email of user like **brittasimon@contoso.com**.</span></span>
       
    > [!NOTE]
    > <span data-ttu-id="7e04a-217">Jeśli chcesz, można ustawić dodatkowe właściwości hello nowy obiekt osoby.</span><span class="sxs-lookup"><span data-stu-id="7e04a-217">If you want to, you can set additional properties of hello new person object.</span></span>
   
    <span data-ttu-id="7e04a-218">c.</span><span class="sxs-lookup"><span data-stu-id="7e04a-218">c.</span></span>  <span data-ttu-id="7e04a-219">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="7e04a-219">Click **Save**.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="7e04a-220">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="7e04a-220">Assign hello Azure AD test user</span></span>

<span data-ttu-id="7e04a-221">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooClickTime.</span><span class="sxs-lookup"><span data-stu-id="7e04a-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooClickTime.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="7e04a-223">**tooassign tooClickTime Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="7e04a-223">**tooassign Britta Simon tooClickTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="7e04a-224">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="7e04a-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="7e04a-226">Z listy aplikacji hello wybierz **ClickTime**.</span><span class="sxs-lookup"><span data-stu-id="7e04a-226">In hello applications list, select **ClickTime**.</span></span>

    ![Łącze ClickTimne na liście aplikacji hello](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. <span data-ttu-id="7e04a-228">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="7e04a-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202] 

4. <span data-ttu-id="7e04a-230">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="7e04a-230">Click **Add** button.</span></span> <span data-ttu-id="7e04a-231">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7e04a-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="7e04a-233">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="7e04a-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="7e04a-234">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7e04a-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7e04a-235">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7e04a-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="7e04a-236">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7e04a-236">Test single sign-on</span></span>

<span data-ttu-id="7e04a-237">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="7e04a-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="7e04a-238">Po kliknięciu kafelka ClickTime hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour ClickTime aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7e04a-238">When you click hello ClickTime tile in hello Access Panel, you should get automatically signed-on tooyour ClickTime application.</span></span>
<span data-ttu-id="7e04a-239">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7e04a-239">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7e04a-240">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="7e04a-240">Additional resources</span></span>

* [<span data-ttu-id="7e04a-241">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7e04a-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7e04a-242">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7e04a-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

