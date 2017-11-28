---
title: 'Samouczek: Integracji Azure Active Directory z UNIFI | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i UNIFI."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e1f49ee4-d2d4-4a82-9baf-0587ca1f20f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: af7cc1167b5c0cff2a1f4cdaa8a2b93f5a718f81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-unifi"></a><span data-ttu-id="d8f22-103">Samouczek: Integracji Azure Active Directory z UNIFI</span><span class="sxs-lookup"><span data-stu-id="d8f22-103">Tutorial: Azure Active Directory integration with UNIFI</span></span>

<span data-ttu-id="d8f22-104">Z tego samouczka, dowiesz się, jak toointegrate UNIFI w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d8f22-104">In this tutorial, you learn how toointegrate UNIFI with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d8f22-105">Integracja z usługą Azure AD UNIFI zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d8f22-105">Integrating UNIFI with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d8f22-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooUNIFI</span><span class="sxs-lookup"><span data-stu-id="d8f22-106">You can control in Azure AD who has access tooUNIFI</span></span>
- <span data-ttu-id="d8f22-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooUNIFI (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8f22-107">You can enable your users tooautomatically get signed-on tooUNIFI (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d8f22-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d8f22-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d8f22-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d8f22-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8f22-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d8f22-110">Prerequisites</span></span>

<span data-ttu-id="d8f22-111">tooconfigure integracji z usługą Azure AD z UNIFI należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d8f22-111">tooconfigure Azure AD integration with UNIFI, you need hello following items:</span></span>

- <span data-ttu-id="d8f22-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8f22-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d8f22-113">UNIFI logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d8f22-113">A UNIFI single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d8f22-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d8f22-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d8f22-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d8f22-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d8f22-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d8f22-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d8f22-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d8f22-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d8f22-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d8f22-118">Scenario description</span></span>
<span data-ttu-id="d8f22-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d8f22-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d8f22-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d8f22-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d8f22-121">Dodawanie UNIFI z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d8f22-121">Adding UNIFI from hello gallery</span></span>
2. <span data-ttu-id="d8f22-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d8f22-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-unifi-from-hello-gallery"></a><span data-ttu-id="d8f22-123">Dodawanie UNIFI z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d8f22-123">Adding UNIFI from hello gallery</span></span>
<span data-ttu-id="d8f22-124">tooconfigure hello integracji UNIFI do usługi Azure AD, należy tooadd UNIFI z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d8f22-124">tooconfigure hello integration of UNIFI into Azure AD, you need tooadd UNIFI from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d8f22-125">**tooadd UNIFI z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d8f22-125">**tooadd UNIFI from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8f22-126">W hello ** [portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d8f22-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="d8f22-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d8f22-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d8f22-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d8f22-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="d8f22-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d8f22-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="d8f22-133">W polu wyszukiwania hello wpisz **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="d8f22-133">In hello search box, type **UNIFI**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_search.png)

5. <span data-ttu-id="d8f22-135">W panelu wyników hello zaznacz **UNIFI**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="d8f22-135">In hello results panel, select **UNIFI**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d8f22-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d8f22-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d8f22-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z UNIFI w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="d8f22-138">In this section, you configure and test Azure AD single sign-on with UNIFI based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d8f22-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w UNIFI jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8f22-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in UNIFI is tooa user in Azure AD.</span></span> <span data-ttu-id="d8f22-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w UNIFI musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="d8f22-140">In other words, a link relationship between an Azure AD user and hello related user in UNIFI needs toobe established.</span></span>

<span data-ttu-id="d8f22-141">W UNIFI, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="d8f22-141">In UNIFI, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="d8f22-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z UNIFI, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d8f22-142">tooconfigure and test Azure AD single sign-on with UNIFI, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d8f22-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on) ** -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d8f22-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d8f22-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user) ** -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d8f22-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d8f22-145">**[Użytkownik testowy tworzenie UNIFI](#creating-a-unifi-test-user) ** -toohave odpowiednikiem Simona Britta w UNIFI, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d8f22-145">**[Creating a UNIFI test user](#creating-a-unifi-test-user)** - toohave a counterpart of Britta Simon in UNIFI that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d8f22-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user) ** -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d8f22-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d8f22-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on) ** -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="d8f22-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d8f22-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d8f22-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d8f22-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji UNIFI.</span><span class="sxs-lookup"><span data-stu-id="d8f22-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your UNIFI application.</span></span>

<span data-ttu-id="d8f22-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z UNIFI, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d8f22-150">**tooconfigure Azure AD single sign-on with UNIFI, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8f22-151">W portalu Azure na powitania hello **UNIFI** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d8f22-151">In hello Azure portal, on hello **UNIFI** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="d8f22-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d8f22-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_samlbase.png)

3. <span data-ttu-id="d8f22-155">Na powitania **UNIFI domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="d8f22-155">On hello **UNIFI Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url1.png)

    <span data-ttu-id="d8f22-157">W hello **identyfikator** pole tekstowe, wartość hello typu:`INVIEWlabs`</span><span class="sxs-lookup"><span data-stu-id="d8f22-157">In hello **Identifier** textbox, type hello value: `INVIEWlabs`</span></span> 

4. <span data-ttu-id="d8f22-158">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**, jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="d8f22-158">Check **Show advanced URL settings**, If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_url2.png)

    <span data-ttu-id="d8f22-160">W hello **adres URL logowania** pole tekstowe, wprowadź adres URL hello:`https://app.discoverunifi.com/login`</span><span class="sxs-lookup"><span data-stu-id="d8f22-160">In hello **Sign-on URL** textbox, type hello URL: `https://app.discoverunifi.com/login`</span></span>

5. <span data-ttu-id="d8f22-161">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d8f22-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_certificate.png) 

6. <span data-ttu-id="d8f22-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d8f22-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-unifi-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="d8f22-165">Na powitania **konfiguracji UNIFI** kliknij **skonfigurować UNIFI** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="d8f22-165">On hello **UNIFI Configuration** section, click **Configure UNIFI** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d8f22-166">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="d8f22-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_configure.png)

8. <span data-ttu-id="d8f22-168">W oknie przeglądarki innej witryny sieci web, zaloguj się na tooyour **UNIFI** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="d8f22-168">In a different web browser window, sign on tooyour **UNIFI** company site as administrator.</span></span>

9. <span data-ttu-id="d8f22-169">Polecenie hello **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="d8f22-169">Click on hello **Users**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-unifi-tutorial/app1.png) 

10. <span data-ttu-id="d8f22-171">Polecenie hello **Dodaj nowego dostawcę tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="d8f22-171">Click on hello **Add New Identity Provider**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-unifi-tutorial/app2.png)

11. <span data-ttu-id="d8f22-173">W hello **Dodawanie dostawcy tożsamości** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d8f22-173">In hello **Add Identity Provider** section, perform hello following steps:</span></span>   

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-unifi-tutorial/app3.png) 

    <span data-ttu-id="d8f22-175">a.</span><span class="sxs-lookup"><span data-stu-id="d8f22-175">a.</span></span> <span data-ttu-id="d8f22-176">W hello **Nazwa dostawcy** pole tekstowe, nazwa typu hello hello dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="d8f22-176">In hello **Provider Name** textbox, type hello name of hello Identity Provider..</span></span>

    <span data-ttu-id="d8f22-177">b.</span><span class="sxs-lookup"><span data-stu-id="d8f22-177">b.</span></span> <span data-ttu-id="d8f22-178">W hello hello **adres URL dostawcy** pole tekstowe Wklej hello **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="d8f22-178">In hello hello **Provider URL** textbox paste hello **SAML Single Sign-On Service URL** value, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d8f22-179">c.</span><span class="sxs-lookup"><span data-stu-id="d8f22-179">c.</span></span> <span data-ttu-id="d8f22-180">Otwórz hello certyfikatu, który został pobrany z portalu Azure w programie Notatnik hello Usuń hello **---BEGIN CERTIFICATE---** i **---END CERTIFICATE---** tag, a następnie wklej hello pozostała zawartość Witaj **certyfikatu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="d8f22-180">Open hello Certificate that you have downloaded from hello Azure portal in notepad, remove hello **---BEGIN CERTIFICATE---** and **---END CERTIFICATE---** tag and then paste hello remaining content in hello **Certificate** textbox.</span></span>

    <span data-ttu-id="d8f22-181">d.</span><span class="sxs-lookup"><span data-stu-id="d8f22-181">d.</span></span> <span data-ttu-id="d8f22-182">Wybierz hello **jest domyślny dostawca** wyboru.</span><span class="sxs-lookup"><span data-stu-id="d8f22-182">Select hello **is Default Provider** checkbox.</span></span>

> [!TIP]
> <span data-ttu-id="d8f22-183">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="d8f22-183">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d8f22-184">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello ** Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="d8f22-184">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d8f22-185">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d8f22-185">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d8f22-186">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8f22-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="d8f22-187">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="d8f22-187">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="d8f22-189">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d8f22-189">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8f22-190">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d8f22-190">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d8f22-192">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d8f22-192">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d8f22-194">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d8f22-194">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d8f22-196">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d8f22-196">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-unifi-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d8f22-198">a.</span><span class="sxs-lookup"><span data-stu-id="d8f22-198">a.</span></span> <span data-ttu-id="d8f22-199">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d8f22-199">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d8f22-200">b.</span><span class="sxs-lookup"><span data-stu-id="d8f22-200">b.</span></span> <span data-ttu-id="d8f22-201">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d8f22-201">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d8f22-202">c.</span><span class="sxs-lookup"><span data-stu-id="d8f22-202">c.</span></span> <span data-ttu-id="d8f22-203">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="d8f22-203">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d8f22-204">d.</span><span class="sxs-lookup"><span data-stu-id="d8f22-204">d.</span></span> <span data-ttu-id="d8f22-205">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d8f22-205">Click **Create**.</span></span>
 
### <a name="creating-a-unifi-test-user"></a><span data-ttu-id="d8f22-206">Tworzenie użytkownika testowego UNIFI</span><span class="sxs-lookup"><span data-stu-id="d8f22-206">Creating a UNIFI test user</span></span>

<span data-ttu-id="d8f22-207">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d8f22-207">In this section, you create a user called Britta Simon.</span></span> <span data-ttu-id="d8f22-208">**UNIFI** obsługę użytkowników, więc nie są wymagane żadne czynności ręcznych.</span><span class="sxs-lookup"><span data-stu-id="d8f22-208">**UNIFI** supports automatic user provisioning so no manual steps are required.</span></span> <span data-ttu-id="d8f22-209">Użytkownicy są tworzone automatycznie po pomyślnym uwierzytelnieniu z hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d8f22-209">Users are created automatically after successful authentication from hello Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d8f22-210">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d8f22-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d8f22-211">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooUNIFI.</span><span class="sxs-lookup"><span data-stu-id="d8f22-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooUNIFI.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="d8f22-213">**tooassign tooUNIFI Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d8f22-213">**tooassign Britta Simon tooUNIFI, perform hello following steps:**</span></span>

1. <span data-ttu-id="d8f22-214">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d8f22-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d8f22-216">Z listy aplikacji hello wybierz **UNIFI**.</span><span class="sxs-lookup"><span data-stu-id="d8f22-216">In hello applications list, select **UNIFI**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-unifi-tutorial/tutorial_unifi_app.png) 

3. <span data-ttu-id="d8f22-218">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d8f22-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="d8f22-220">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d8f22-220">Click **Add** button.</span></span> <span data-ttu-id="d8f22-221">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d8f22-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="d8f22-223">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d8f22-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d8f22-224">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d8f22-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d8f22-225">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d8f22-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d8f22-226">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d8f22-226">Testing single sign-on</span></span>

<span data-ttu-id="d8f22-227">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d8f22-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="d8f22-228">Po kliknięciu hello UNIFI kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour UNIFI aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d8f22-228">When you click hello UNIFI tile in hello Access Panel, you should get automatically signed-on tooyour UNIFI application.</span></span>
<span data-ttu-id="d8f22-229">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d8f22-229">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="d8f22-230">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d8f22-230">Additional resources</span></span>

* [<span data-ttu-id="d8f22-231">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8f22-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d8f22-232">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d8f22-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-unifi-tutorial/tutorial_general_203.png

