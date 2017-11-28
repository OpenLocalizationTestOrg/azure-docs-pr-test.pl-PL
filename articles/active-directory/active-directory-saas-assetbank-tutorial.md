---
title: "Samouczek: Integracji Azure Active Directory z zasobów Bank | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Bank zasobów."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3006ad6e-8831-41cd-94aa-7e7ae770ce7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 32cb355fbe16557eca69dbad1d3e6fbe19b53517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asset-bank"></a><span data-ttu-id="b9ef0-103">Samouczek: Integracji Azure Active Directory z banku zasobów</span><span class="sxs-lookup"><span data-stu-id="b9ef0-103">Tutorial: Azure Active Directory integration with Asset Bank</span></span>

<span data-ttu-id="b9ef0-104">Z tego samouczka, dowiesz się, jak toointegrate Bankowi zasobów w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b9ef0-104">In this tutorial, you learn how toointegrate Asset Bank with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b9ef0-105">Integrowanie Bank zasobów z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="b9ef0-105">Integrating Asset Bank with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b9ef0-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooAsset Bank</span><span class="sxs-lookup"><span data-stu-id="b9ef0-106">You can control in Azure AD who has access tooAsset Bank</span></span>
- <span data-ttu-id="b9ef0-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooAsset Bank (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9ef0-107">You can enable your users tooautomatically get signed-on tooAsset Bank (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b9ef0-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="b9ef0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b9ef0-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b9ef0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9ef0-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b9ef0-110">Prerequisites</span></span>

<span data-ttu-id="b9ef0-111">tooconfigure integracji usługi Azure AD z banku zasobów należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b9ef0-111">tooconfigure Azure AD integration with Asset Bank, you need hello following items:</span></span>

- <span data-ttu-id="b9ef0-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9ef0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b9ef0-113">Bank zasobów jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b9ef0-113">An Asset Bank single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b9ef0-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b9ef0-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="b9ef0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b9ef0-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b9ef0-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b9ef0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b9ef0-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="b9ef0-118">Scenario description</span></span>
<span data-ttu-id="b9ef0-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b9ef0-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="b9ef0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b9ef0-121">Dodawanie zasobów Bank z galerii hello</span><span class="sxs-lookup"><span data-stu-id="b9ef0-121">Adding Asset Bank from hello gallery</span></span>
2. <span data-ttu-id="b9ef0-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b9ef0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asset-bank-from-hello-gallery"></a><span data-ttu-id="b9ef0-123">Dodawanie zasobów Bank z galerii hello</span><span class="sxs-lookup"><span data-stu-id="b9ef0-123">Adding Asset Bank from hello gallery</span></span>
<span data-ttu-id="b9ef0-124">tooconfigure hello integracji Bank zasobów w usłudze Azure Active Directory, należy tooadd Bank zasobów z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-124">tooconfigure hello integration of Asset Bank into Azure AD, you need tooadd Asset Bank from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b9ef0-125">**tooadd Bank zasobów z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b9ef0-125">**tooadd Asset Bank from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9ef0-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="b9ef0-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b9ef0-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="b9ef0-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="b9ef0-133">W polu wyszukiwania hello wpisz **Bank zasobów**.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-133">In hello search box, type **Asset Bank**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_search.png)

5. <span data-ttu-id="b9ef0-135">W panelu wyników hello, wybierz **Bank zasobów**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-135">In hello results panel, select **Asset Bank**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b9ef0-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b9ef0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b9ef0-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej banku zasobów na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="b9ef0-138">In this section, you configure and test Azure AD single sign-on with Asset Bank based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b9ef0-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w banku zasobów jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Asset Bank is tooa user in Azure AD.</span></span> <span data-ttu-id="b9ef0-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w banku zasobów musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-140">In other words, a link relationship between an Azure AD user and hello related user in Asset Bank needs toobe established.</span></span>

<span data-ttu-id="b9ef0-141">W banku zasobów, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-141">In Asset Bank, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b9ef0-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej w banku zasobów, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b9ef0-142">tooconfigure and test Azure AD single sign-on with Asset Bank, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b9ef0-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b9ef0-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b9ef0-145">**[Tworzenie użytkownika testowego Bank zasobów](#creating-an-asset-bank-test-user)**  -toohave odpowiednikiem Simona Britta w banku zasobów, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-145">**[Creating an Asset Bank test user](#creating-an-asset-bank-test-user)** - toohave a counterpart of Britta Simon in Asset Bank that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b9ef0-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b9ef0-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b9ef0-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b9ef0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b9ef0-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w banku zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Asset Bank application.</span></span>

<span data-ttu-id="b9ef0-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z banku zasobów, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b9ef0-150">**tooconfigure Azure AD single sign-on with Asset Bank, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9ef0-151">W portalu Azure na powitania hello **Bank zasobów** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-151">In hello Azure portal, on hello **Asset Bank** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="b9ef0-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_samlbase.png)

3. <span data-ttu-id="b9ef0-155">Na powitania **zasobów Bank domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="b9ef0-155">On hello **Asset Bank Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_url.png)

    <span data-ttu-id="b9ef0-157">a.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-157">a.</span></span> <span data-ttu-id="b9ef0-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.assetbank-server.com`</span><span class="sxs-lookup"><span data-stu-id="b9ef0-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.assetbank-server.com`</span></span>

    <span data-ttu-id="b9ef0-159">b.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-159">b.</span></span> <span data-ttu-id="b9ef0-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<companyname>.assetbank-server.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="b9ef0-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.assetbank-server.com/shibboleth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b9ef0-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-161">These values are not real.</span></span> <span data-ttu-id="b9ef0-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b9ef0-163">Skontaktuj się z [zespołem pomocy technicznej klienta Bank zasobów](mailto:support@assetbank.co.uk) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-163">Contact [Asset Bank Client support team](mailto:support@assetbank.co.uk) tooget these values.</span></span> 
 
4. <span data-ttu-id="b9ef0-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_certificate.png) 

5. <span data-ttu-id="b9ef0-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-assetbank-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b9ef0-168">tooconfigure rejestracji jednokrotnej w **Bank zasobów** strony, należy pobrać hello toosend **XML metadanych** za[zespołem pomocy technicznej Bank zasobów](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="b9ef0-168">tooconfigure single sign-on on **Asset Bank** side, you need toosend hello downloaded **Metadata XML** too[Asset Bank support team](mailto:support@assetbank.co.uk).</span></span> 


> [!TIP]
> <span data-ttu-id="b9ef0-169">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="b9ef0-169">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b9ef0-170">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-170">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b9ef0-171">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b9ef0-171">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b9ef0-172">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9ef0-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="b9ef0-173">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-173">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="b9ef0-175">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b9ef0-175">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9ef0-176">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-176">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b9ef0-178">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-178">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b9ef0-180">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-180">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b9ef0-182">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b9ef0-182">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b9ef0-184">a.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-184">a.</span></span> <span data-ttu-id="b9ef0-185">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-185">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b9ef0-186">b.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-186">b.</span></span> <span data-ttu-id="b9ef0-187">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-187">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b9ef0-188">c.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-188">c.</span></span> <span data-ttu-id="b9ef0-189">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-189">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b9ef0-190">d.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-190">d.</span></span> <span data-ttu-id="b9ef0-191">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-191">Click **Create**.</span></span>
 
### <a name="creating-an-asset-bank-test-user"></a><span data-ttu-id="b9ef0-192">Tworzenie użytkownika testowego Bank zasobów</span><span class="sxs-lookup"><span data-stu-id="b9ef0-192">Creating an Asset Bank test user</span></span>

<span data-ttu-id="b9ef0-193">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w banku zasobów.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-193">hello objective of this section is toocreate a user called Britta Simon in Asset Bank.</span></span> <span data-ttu-id="b9ef0-194">Bank zasobów obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-194">Asset Bank supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="b9ef0-195">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-195">There is no action item for you in this section.</span></span> <span data-ttu-id="b9ef0-196">Nowy użytkownik został utworzony podczas tooaccess próba Bank zasobów, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-196">A new user is created during an attempt tooaccess Asset Bank if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="b9ef0-197">Jeśli potrzebujesz ręcznie toocreate użytkownika, należy toocontact hello [zespołem pomocy technicznej Bank zasobów](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="b9ef0-197">If you need toocreate a user manually, you need toocontact hello [Asset Bank support team](mailto:support@assetbank.co.uk).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b9ef0-198">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9ef0-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b9ef0-199">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooAsset Bank.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAsset Bank.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="b9ef0-201">**tooassign tooAsset Simona Britta Bank, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b9ef0-201">**tooassign Britta Simon tooAsset Bank, perform hello following steps:**</span></span>

1. <span data-ttu-id="b9ef0-202">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="b9ef0-204">Z listy aplikacji hello wybierz **Bank zasobów**.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-204">In hello applications list, select **Asset Bank**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_app.png) 

3. <span data-ttu-id="b9ef0-206">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="b9ef0-208">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-208">Click **Add** button.</span></span> <span data-ttu-id="b9ef0-209">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="b9ef0-211">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b9ef0-212">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b9ef0-213">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b9ef0-214">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b9ef0-214">Testing single sign-on</span></span>

<span data-ttu-id="b9ef0-215">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-215">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b9ef0-216">Po kliknięciu kafelka Bank zasobów hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Bank zasobów aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b9ef0-216">When you click hello Asset Bank tile in hello Access Panel, you should get automatically signed-on tooyour Asset Bank application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b9ef0-217">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b9ef0-217">Additional resources</span></span>

* [<span data-ttu-id="b9ef0-218">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b9ef0-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b9ef0-219">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b9ef0-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_203.png

