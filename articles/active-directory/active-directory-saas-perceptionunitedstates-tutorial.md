---
title: "Samouczek: Integracji Azure Active Directory z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro) | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Stanów Zjednoczonych z punktu widzenia użytkownika (Non-UltiPro)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 874b5da277b9c68504c4af2ac87ed90d2bbd93b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a><span data-ttu-id="e6cfe-103">Samouczek: Integracji Azure Active Directory z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro)</span><span class="sxs-lookup"><span data-stu-id="e6cfe-103">Tutorial: Azure Active Directory integration with Perception United States (Non-UltiPro)</span></span>

<span data-ttu-id="e6cfe-104">Z tego samouczka, dowiesz się, jak toointegrate wrażenie Stanów Zjednoczonych (Non-UltiPro) w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e6cfe-104">In this tutorial, you learn how toointegrate Perception United States (Non-UltiPro) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e6cfe-105">Integrowanie z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro) z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e6cfe-105">Integrating Perception United States (Non-UltiPro) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e6cfe-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooPerception Stanów Zjednoczonych (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="e6cfe-106">You can control in Azure AD who has access tooPerception United States (Non-UltiPro).</span></span>
- <span data-ttu-id="e6cfe-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooPerception Stanów Zjednoczonych (Non-UltiPro) (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-107">You can enable your users tooautomatically get signed-on tooPerception United States (Non-UltiPro) (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e6cfe-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="e6cfe-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e6cfe-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6cfe-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e6cfe-110">Prerequisites</span></span>

<span data-ttu-id="e6cfe-111">tooconfigure integracji z usługą Azure AD z punktu widzenia użytkownika Stany Zjednoczone (inne niż UltiPro), należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e6cfe-111">tooconfigure Azure AD integration with Perception United States (Non-UltiPro), you need hello following items:</span></span>

- <span data-ttu-id="e6cfe-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e6cfe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e6cfe-113">Z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro) logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e6cfe-113">A Perception United States (Non-UltiPro) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e6cfe-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e6cfe-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e6cfe-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e6cfe-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e6cfe-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e6cfe-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e6cfe-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e6cfe-118">Scenario description</span></span>
<span data-ttu-id="e6cfe-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e6cfe-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e6cfe-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e6cfe-121">Dodawanie z galerii hello wrażenie Stany Zjednoczone (Non-UltiPro)</span><span class="sxs-lookup"><span data-stu-id="e6cfe-121">Adding Perception United States (Non-UltiPro) from hello gallery</span></span>
2. <span data-ttu-id="e6cfe-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e6cfe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-perception-united-states-non-ultipro-from-hello-gallery"></a><span data-ttu-id="e6cfe-123">Dodawanie z galerii hello wrażenie Stany Zjednoczone (Non-UltiPro)</span><span class="sxs-lookup"><span data-stu-id="e6cfe-123">Adding Perception United States (Non-UltiPro) from hello gallery</span></span>
<span data-ttu-id="e6cfe-124">tooconfigure hello integracji z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro) do usługi Azure AD, należy tooadd wrażenie Stany Zjednoczone (Non-UltiPro) z listy tooyour galerii hello zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-124">tooconfigure hello integration of Perception United States (Non-UltiPro) into Azure AD, you need tooadd Perception United States (Non-UltiPro) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e6cfe-125">**tooadd wrażenie Stany Zjednoczone (Non-UltiPro) z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e6cfe-125">**tooadd Perception United States (Non-UltiPro) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e6cfe-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="e6cfe-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e6cfe-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="e6cfe-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="e6cfe-133">W hello wyszukiwania wpisz **wrażenie Stany Zjednoczone (Non-UltiPro)**, wybierz pozycję **wrażenie Stany Zjednoczone (Non-UltiPro)** z panelu wyników kliknięcie **Dodaj** tooadd przycisk Aplikacja Hello.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-133">In hello search box, type **Perception United States (Non-UltiPro)**, select **Perception United States (Non-UltiPro)** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro) na liście wyników hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e6cfe-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e6cfe-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e6cfe-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z punktu widzenia użytkownika Stanów Zjednoczonych (Non-UltiPro) w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-136">In this section, you configure and test Azure AD single sign-on with Perception United States (Non-UltiPro) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e6cfe-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello używanego w Stanach Zjednoczonych z punktu widzenia użytkownika (Non-UltiPro) jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Perception United States (Non-UltiPro) is tooa user in Azure AD.</span></span> <span data-ttu-id="e6cfe-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Stanach Zjednoczonych z punktu widzenia użytkownika (Non-UltiPro) musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-138">In other words, a link relationship between an Azure AD user and hello related user in Perception United States (Non-UltiPro) needs toobe established.</span></span>

<span data-ttu-id="e6cfe-139">W wrażenie Stanów Zjednoczonych (inne niż UltiPro), przypisz wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-139">In Perception United States (Non-UltiPro), assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e6cfe-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z punktu widzenia użytkownika Stany Zjednoczone (inne niż UltiPro), należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="e6cfe-140">tooconfigure and test Azure AD single sign-on with Perception United States (Non-UltiPro), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e6cfe-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e6cfe-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e6cfe-143">**[Tworzenie użytkownika testowego z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro)](#create-a-perception-united-states-non-ultipro-test-user)**  -toohave odpowiednikiem Simona Britta w wrażenie Stanów Zjednoczonych (inne niż UltiPro), który jest odpowiednikiem połączonych toohello usługi Azure AD użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-143">**[Create a Perception United States (Non-UltiPro) test user](#create-a-perception-united-states-non-ultipro-test-user)** - toohave a counterpart of Britta Simon in Perception United States (Non-UltiPro) that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e6cfe-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e6cfe-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e6cfe-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e6cfe-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e6cfe-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="e6cfe-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Perception United States (Non-UltiPro) application.</span></span>

<span data-ttu-id="e6cfe-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro), wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e6cfe-148">**tooconfigure Azure AD single sign-on with Perception United States (Non-UltiPro), perform hello following steps:**</span></span>

1. <span data-ttu-id="e6cfe-149">W portalu Azure na powitania hello **wrażenie Stany Zjednoczone (Non-UltiPro)** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-149">In hello Azure portal, on hello **Perception United States (Non-UltiPro)** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="e6cfe-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

3. <span data-ttu-id="e6cfe-153">Na powitania **domeny wrażenie Stany Zjednoczone (Non-UltiPro) i adresy URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e6cfe-153">On hello **Perception United States (Non-UltiPro) Domain and URLs** section, perform hello following steps:</span></span>

    ![Z punktu widzenia użytkownika domeny Stanów Zjednoczonych (Non-UltiPro) i adres URL z jednym informacje logowania jednokrotnego](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    <span data-ttu-id="e6cfe-155">a.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-155">a.</span></span> <span data-ttu-id="e6cfe-156">W hello **identyfikator** pole tekstowe, wprowadź adres URL hello:`https://perception.kanjoya.com/sp`</span><span class="sxs-lookup"><span data-stu-id="e6cfe-156">In hello **Identifier** textbox, type hello URL: `https://perception.kanjoya.com/sp`</span></span>

    <span data-ttu-id="e6cfe-157">b.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-157">b.</span></span> <span data-ttu-id="e6cfe-158">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://perception.kanjoya.com/sso?idp=<entity_id>`</span><span class="sxs-lookup"><span data-stu-id="e6cfe-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://perception.kanjoya.com/sso?idp=<entity_id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e6cfe-159">wartość Hello nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-159">hello value is not real.</span></span> <span data-ttu-id="e6cfe-160">Wartość hello zostanie zaktualizowany hello rzeczywiste odpowiedzi adresu URL, który znajduje się w dalszej części samouczka hello.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-160">You will update hello value with hello actual Reply URL, which is explained later in hello tutorial.</span></span>
 
4. <span data-ttu-id="e6cfe-161">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

5. <span data-ttu-id="e6cfe-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-163">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e6cfe-165">Na powitania **konfiguracji wrażenie Stany Zjednoczone (Non-UltiPro)** , kliknij przycisk **skonfigurować wrażenie Stany Zjednoczone (Non-UltiPro)** tooopen **Konfigurowanie logowania jednokrotnego** okno.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-165">On hello **Perception United States (Non-UltiPro) Configuration** section, click **Configure Perception United States (Non-UltiPro)** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="e6cfe-166">Kopiuj hello **SAML identyfikator jednostki** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="e6cfe-166">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    <span data-ttu-id="e6cfe-167">a.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-167">a.</span></span> <span data-ttu-id="e6cfe-168">Hello **wrażenie Stany Zjednoczone (Non-UltiPro)** aplikacja wymaga hello **identyfikator jednostki SAML** kodowany identyfikator uri toobe wartość, która została skopiowana,.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-168">hello **Perception United States (Non-UltiPro)** application requires hello **SAML Entity ID** value, which you have copied, toobe uri encoded.</span></span> <span data-ttu-id="e6cfe-169">wartość identyfikatora uri zakodowane hello tooget, użyj hello łącza:**http://www.url-encode-decode.com/**.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-169">tooget hello uri encoded value, use hello following link:**http://www.url-encode-decode.com/**.</span></span>

    <span data-ttu-id="e6cfe-170">b.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-170">b.</span></span> <span data-ttu-id="e6cfe-171">Po pierwsze hello uri zakodowaną wartość połączyć ją z hello **adres URL odpowiedzi** wymienionych poniżej -</span><span class="sxs-lookup"><span data-stu-id="e6cfe-171">After getting hello uri encoded value combine it with hello **Reply URL** as mentioned below-</span></span>

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    <span data-ttu-id="e6cfe-172">c.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-172">c.</span></span> <span data-ttu-id="e6cfe-173">Wklej hello większa niż wartość w hello **adres URL odpowiedzi** textbox w **domeny wrażenie Stany Zjednoczone (Non-UltiPro) i adresy URL** sekcji.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-173">Paste hello above value in hello **Reply URL** textbox in **Perception United States (Non-UltiPro) Domain and URLs** section.</span></span>

    ![Konfiguracja Stanów Zjednoczonych (z systemem innym niż UltiPro) z punktu widzenia użytkownika](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

7. <span data-ttu-id="e6cfe-175">W innym oknie przeglądarki Zaloguj się w witrynie firmy wrażenie Stany Zjednoczone (Non-UltiPro) tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-175">In another browser window, sign on tooyour Perception United States (Non-UltiPro) company site as an administrator.</span></span>

8. <span data-ttu-id="e6cfe-176">Witaj głównym pasku narzędzi, kliknij przycisk **ustawienia konta**.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-176">In hello main toolbar, click **Account Settings**.</span></span>

    ![Użytkownik Stanów Zjednoczonych (Non-UltiPro) z punktu widzenia użytkownika](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

9. <span data-ttu-id="e6cfe-178">Na powitania **ustawienia konta** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e6cfe-178">On hello **Account Settings** page, perform hello following steps:</span></span>

    ![Użytkownik Stanów Zjednoczonych (Non-UltiPro) z punktu widzenia użytkownika](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    <span data-ttu-id="e6cfe-180">a.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-180">a.</span></span> <span data-ttu-id="e6cfe-181">W hello **nazwa firmy** pole tekstowe, nazwa typu hello hello **firmy**.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-181">In hello **Company Name** textbox, type hello name of hello **Company**.</span></span>
    
    <span data-ttu-id="e6cfe-182">b.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-182">b.</span></span> <span data-ttu-id="e6cfe-183">W hello **nazwa konta** pole tekstowe, nazwa typu hello hello **konta**.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-183">In hello **Account Name** textbox, type hello name of hello **Account**.</span></span>

    <span data-ttu-id="e6cfe-184">c.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-184">c.</span></span> <span data-ttu-id="e6cfe-185">W **domyślne odpowiedzi tooEmail** pole tekstowe, hello typu, prawidłową **E-mail**.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-185">In **Default Reply-tooEmail** text box, type hello valid **Email**.</span></span>

    <span data-ttu-id="e6cfe-186">d.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-186">d.</span></span> <span data-ttu-id="e6cfe-187">Wybierz **dostawcy tożsamości logowania jednokrotnego** jako **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-187">Select **SSO Identity Provider** as **SAML 2.0**.</span></span>

10. <span data-ttu-id="e6cfe-188">Na powitania **konfiguracji logowania jednokrotnego** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e6cfe-188">On hello **SSO Configuration** page, perform hello following steps:</span></span>

    ![SSOConfig Stanów Zjednoczonych (z systemem innym niż UltiPro) z punktu widzenia użytkownika](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    <span data-ttu-id="e6cfe-190">a.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-190">a.</span></span> <span data-ttu-id="e6cfe-191">Wybierz **typu NameID SAML** jako **E-mail**.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-191">Select **SAML NameID Type** as **EMAIL**.</span></span>

    <span data-ttu-id="e6cfe-192">b.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-192">b.</span></span> <span data-ttu-id="e6cfe-193">W hello **Nazwa konfiguracji logowania jednokrotnego** pole tekstowe, nazwa typu hello Twojej **konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-193">In hello **SSO Configuration Name** textbox, type hello name of your **Configuration**.</span></span>
    
    <span data-ttu-id="e6cfe-194">c.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-194">c.</span></span> <span data-ttu-id="e6cfe-195">W **Nazwa dostawcy tożsamości** pole tekstowe, Wklej wartość hello **identyfikator jednostki SAML**, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-195">In **Identity Provider Name** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="e6cfe-196">d.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-196">d.</span></span> <span data-ttu-id="e6cfe-197">W **textbox domeny SAML**, wprowadź domenę hello, takich jak  **@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="e6cfe-197">In **SAML Domain textbox**, enter hello domain like **@contoso.com**.</span></span>

    <span data-ttu-id="e6cfe-198">e.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-198">e.</span></span> <span data-ttu-id="e6cfe-199">Polecenie **Przekaż ponownie** tooupload hello **XML metadanych** pliku.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-199">Click on **Upload Again** tooupload hello **Metadata XML** file.</span></span>

    <span data-ttu-id="e6cfe-200">f.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-200">f.</span></span> <span data-ttu-id="e6cfe-201">Kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-201">Click **Update**.</span></span>


> [!TIP]
> <span data-ttu-id="e6cfe-202">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="e6cfe-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e6cfe-203">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e6cfe-204">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e6cfe-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e6cfe-205">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e6cfe-205">Create an Azure AD test user</span></span>

<span data-ttu-id="e6cfe-206">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="e6cfe-208">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e6cfe-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e6cfe-209">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e6cfe-211">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e6cfe-213">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e6cfe-215">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e6cfe-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-perceptionunitedstates-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e6cfe-217">a.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-217">a.</span></span> <span data-ttu-id="e6cfe-218">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e6cfe-219">b.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-219">b.</span></span> <span data-ttu-id="e6cfe-220">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="e6cfe-221">c.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-221">c.</span></span> <span data-ttu-id="e6cfe-222">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="e6cfe-223">d.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-223">d.</span></span> <span data-ttu-id="e6cfe-224">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-224">Click **Create**.</span></span>
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a><span data-ttu-id="e6cfe-225">Tworzenie użytkownika testowego z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro)</span><span class="sxs-lookup"><span data-stu-id="e6cfe-225">Create a Perception United States (Non-UltiPro) test user</span></span>

<span data-ttu-id="e6cfe-226">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Stanach Zjednoczonych z punktu widzenia użytkownika (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="e6cfe-226">In this section, you create a user called Britta Simon in Perception United States (Non-UltiPro).</span></span> <span data-ttu-id="e6cfe-227">Praca z [zespołem pomocy technicznej z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro)](http://www.ultimatesoftware.com/Contact/ContactUs) użytkowników hello tooadd hello wrażenie Stany Zjednoczone (Non-UltiPro) platformy.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-227">Work with [Perception United States (Non-UltiPro) support team](http://www.ultimatesoftware.com/Contact/ContactUs) tooadd hello users in hello Perception United States (Non-UltiPro) platform.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="e6cfe-228">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e6cfe-228">Assign hello Azure AD test user</span></span>

<span data-ttu-id="e6cfe-229">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooPerception Stany Zjednoczone (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="e6cfe-229">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPerception United States (Non-UltiPro).</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="e6cfe-231">**tooassign Simona Britta tooPerception Stany Zjednoczone (Non-UltiPro), wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e6cfe-231">**tooassign Britta Simon tooPerception United States (Non-UltiPro), perform hello following steps:**</span></span>

1. <span data-ttu-id="e6cfe-232">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-232">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e6cfe-234">Z listy aplikacji hello wybierz **wrażenie Stany Zjednoczone (Non-UltiPro)**.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-234">In hello applications list, select **Perception United States (Non-UltiPro)**.</span></span>

    ![łącze wrażenie Stany Zjednoczone (Non-UltiPro) Hello na liście aplikacji hello](./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

3. <span data-ttu-id="e6cfe-236">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-236">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="e6cfe-238">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-238">Click **Add** button.</span></span> <span data-ttu-id="e6cfe-239">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-239">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="e6cfe-241">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-241">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e6cfe-242">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-242">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e6cfe-243">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-243">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e6cfe-244">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e6cfe-244">Test single sign-on</span></span>

<span data-ttu-id="e6cfe-245">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="e6cfe-245">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e6cfe-246">Po kliknięciu kafelka wrażenie Stany Zjednoczone (Non-UltiPro) hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour aplikacji z punktu widzenia użytkownika Stany Zjednoczone (Non-UltiPro).</span><span class="sxs-lookup"><span data-stu-id="e6cfe-246">When you click hello Perception United States (Non-UltiPro) tile in hello Access Panel, you should get automatically signed-on tooyour Perception United States (Non-UltiPro) application.</span></span>
<span data-ttu-id="e6cfe-247">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e6cfe-247">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e6cfe-248">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e6cfe-248">Additional resources</span></span>

* [<span data-ttu-id="e6cfe-249">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e6cfe-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e6cfe-250">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e6cfe-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-perceptionunitedstates-tutorial/tutorial_general_203.png

