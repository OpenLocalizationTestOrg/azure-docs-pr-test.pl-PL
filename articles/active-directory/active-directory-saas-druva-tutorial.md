---
title: 'Samouczek: Integracji Azure Active Directory z Druva | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Druva."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: ab92b600-1fea-4905-b1c7-ef8e4d8c495c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: a1c36c06d6d005e0aa363fbf34efe630e4cca1ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-druva"></a><span data-ttu-id="9b052-103">Samouczek: Integracji Azure Active Directory z Druva</span><span class="sxs-lookup"><span data-stu-id="9b052-103">Tutorial: Azure Active Directory integration with Druva</span></span>

<span data-ttu-id="9b052-104">Z tego samouczka, dowiesz się, jak toointegrate Druva w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9b052-104">In this tutorial, you learn how toointegrate Druva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9b052-105">Integracja z usługą Azure AD Druva zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="9b052-105">Integrating Druva with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9b052-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooDruva.</span><span class="sxs-lookup"><span data-stu-id="9b052-106">You can control in Azure AD who has access tooDruva.</span></span>
- <span data-ttu-id="9b052-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooDruva (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b052-107">You can enable your users tooautomatically get signed-on tooDruva (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="9b052-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9b052-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="9b052-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9b052-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b052-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9b052-110">Prerequisites</span></span>

<span data-ttu-id="9b052-111">tooconfigure integracji z usługą Azure AD z Druva należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9b052-111">tooconfigure Azure AD integration with Druva, you need hello following items:</span></span>

- <span data-ttu-id="9b052-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b052-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9b052-113">Druva logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9b052-113">A Druva single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9b052-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="9b052-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9b052-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="9b052-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9b052-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9b052-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9b052-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9b052-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9b052-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="9b052-118">Scenario description</span></span>
<span data-ttu-id="9b052-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="9b052-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9b052-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="9b052-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9b052-121">Dodawanie Druva z galerii hello</span><span class="sxs-lookup"><span data-stu-id="9b052-121">Adding Druva from hello gallery</span></span>
2. <span data-ttu-id="9b052-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9b052-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-druva-from-hello-gallery"></a><span data-ttu-id="9b052-123">Dodawanie Druva z galerii hello</span><span class="sxs-lookup"><span data-stu-id="9b052-123">Adding Druva from hello gallery</span></span>
<span data-ttu-id="9b052-124">tooconfigure hello integracji Druva do usługi Azure AD, należy tooadd Druva z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="9b052-124">tooconfigure hello integration of Druva into Azure AD, you need tooadd Druva from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9b052-125">**tooadd Druva z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9b052-125">**tooadd Druva from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b052-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9b052-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="9b052-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="9b052-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9b052-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9b052-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="9b052-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9b052-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="9b052-133">W polu wyszukiwania hello wpisz **Druva**, wybierz pozycję **Druva** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="9b052-133">In hello search box, type **Druva**, select **Druva** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Druva hello listy wyników](./media/active-directory-saas-druva-tutorial/tutorial_druva_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="9b052-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9b052-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="9b052-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Druva w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="9b052-136">In this section, you configure and test Azure AD single sign-on with Druva based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="9b052-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Druva jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b052-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Druva is tooa user in Azure AD.</span></span> <span data-ttu-id="9b052-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Druva musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="9b052-138">In other words, a link relationship between an Azure AD user and hello related user in Druva needs toobe established.</span></span>

<span data-ttu-id="9b052-139">W Druva, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="9b052-139">In Druva, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9b052-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Druva, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="9b052-140">tooconfigure and test Azure AD single sign-on with Druva, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9b052-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="9b052-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9b052-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9b052-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9b052-143">**[Tworzenie użytkownika testowego Druva](#create-a-druva-test-user)**  -toohave odpowiednikiem Simona Britta w Druva, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9b052-143">**[Create a Druva test user](#create-a-druva-test-user)** - toohave a counterpart of Britta Simon in Druva that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9b052-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9b052-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9b052-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="9b052-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="9b052-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9b052-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="9b052-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Druva.</span><span class="sxs-lookup"><span data-stu-id="9b052-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Druva application.</span></span>

<span data-ttu-id="9b052-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Druva, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9b052-148">**tooconfigure Azure AD single sign-on with Druva, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b052-149">W portalu Azure na powitania hello **Druva** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="9b052-149">In hello Azure portal, on hello **Druva** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="9b052-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9b052-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-druva-tutorial/tutorial_druva_samlbase.png)

3. <span data-ttu-id="9b052-153">Na powitania **Druva domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9b052-153">On hello **Druva Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-druva-tutorial/tutorial_druva_url.png)

    <span data-ttu-id="9b052-155">W hello **adres URL logowania** pole tekstowe, wprowadź adres URL hello:`https://cloud.druva.com/home`</span><span class="sxs-lookup"><span data-stu-id="9b052-155">In hello **Sign-on URL** textbox, type hello URL: `https://cloud.druva.com/home`</span></span>

4. <span data-ttu-id="9b052-156">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="9b052-156">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-druva-tutorial/tutorial_druva_certificate.png) 

5. <span data-ttu-id="9b052-158">Aplikacja Druva oczekuje potwierdzenia SAML hello w określonym formacie wymaga tooyour mapowań atrybutów niestandardowych tooadd **atrybuty tokenu SAML** konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="9b052-158">Your Druva application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **SAML Token Attributes** configuration.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-druva-tutorial/tutorial_druva_attribute.png)

6. <span data-ttu-id="9b052-160">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, Konfigurowanie atrybutu tokenu SAML, jak pokazano w hello poprzedzających obrazu i wykonywanie hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9b052-160">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>

    | <span data-ttu-id="9b052-161">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="9b052-161">Attribute Name</span></span>      | <span data-ttu-id="9b052-162">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="9b052-162">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="9b052-163">zsynchronizowana\_uwierzytelniania\_tokenu</span><span class="sxs-lookup"><span data-stu-id="9b052-163">insync\_auth\_token</span></span> |<span data-ttu-id="9b052-164">Wprowadź wartość tokenu wygenerowanego hello</span><span class="sxs-lookup"><span data-stu-id="9b052-164">Enter hello token generated value</span></span> |
    
    <span data-ttu-id="9b052-165">a.</span><span class="sxs-lookup"><span data-stu-id="9b052-165">a.</span></span> <span data-ttu-id="9b052-166">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9b052-166">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-druva-tutorial/tutorial_attribute_04.png)
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-druva-tutorial/tutorial_attribute_05.png)
    
    <span data-ttu-id="9b052-169">b.</span><span class="sxs-lookup"><span data-stu-id="9b052-169">b.</span></span> <span data-ttu-id="9b052-170">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="9b052-170">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="9b052-171">c.</span><span class="sxs-lookup"><span data-stu-id="9b052-171">c.</span></span> <span data-ttu-id="9b052-172">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="9b052-172">From hello **Value** list, type hello attribute value shown for that row.</span></span> <span data-ttu-id="9b052-173">tłumaczy wartość tokenu wygenerowanego Hello później w samouczku.</span><span class="sxs-lookup"><span data-stu-id="9b052-173">hello token generated value is explained later in tutorial.</span></span>
    
    <span data-ttu-id="9b052-174">d.</span><span class="sxs-lookup"><span data-stu-id="9b052-174">d.</span></span> <span data-ttu-id="9b052-175">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="9b052-175">Click **Ok**.</span></span>    

7. <span data-ttu-id="9b052-176">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9b052-176">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-druva-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="9b052-178">Na powitania **konfiguracji Druva** kliknij **skonfigurować Druva** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="9b052-178">On hello **Druva Configuration** section, click **Configure Druva** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="9b052-179">Kopiuj hello **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="9b052-179">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-druva-tutorial/tutorial_druva_configure.png) 

9. <span data-ttu-id="9b052-181">W oknie przeglądarki innej witryny sieci web Zaloguj się w witrynie firmy Druva tooyour jako administrator.</span><span class="sxs-lookup"><span data-stu-id="9b052-181">In a different web browser window, log in tooyour Druva company site as an administrator.</span></span>

10. <span data-ttu-id="9b052-182">Przejdź za**Zarządzaj \> ustawienia**.</span><span class="sxs-lookup"><span data-stu-id="9b052-182">Go too**Manage \> Settings**.</span></span>

    <span data-ttu-id="9b052-183">![Ustawienia](./media/active-directory-saas-druva-tutorial/ic795091.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="9b052-183">![Settings](./media/active-directory-saas-druva-tutorial/ic795091.png "Settings")</span></span>

11. <span data-ttu-id="9b052-184">W oknie dialogowym Ustawienia rejestracji jednokrotnej hello wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9b052-184">On hello Single Sign-On Settings dialog, perform hello following steps:</span></span>

    <span data-ttu-id="9b052-185">![Single Sign-On ustawienia](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On ustawienia")</span><span class="sxs-lookup"><span data-stu-id="9b052-185">![Single Sign-On Settings](./media/active-directory-saas-druva-tutorial/ic795092.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="9b052-186">a.</span><span class="sxs-lookup"><span data-stu-id="9b052-186">a.</span></span> <span data-ttu-id="9b052-187">Wklej **SAML pojedynczy znak na adres URL usługi** wartość, która została skopiowana z hello portalu Azure do hello **adres URL logowania dostawcy identyfikator** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9b052-187">Paste **SAML Single Sign-On Service URL** value, which you have copied from hello Azure portal into hello **ID Provider Login URL** textbox.</span></span>
    
    <span data-ttu-id="9b052-188">b.</span><span class="sxs-lookup"><span data-stu-id="9b052-188">b.</span></span> <span data-ttu-id="9b052-189">Wklej **Sign-Out URL** wartość, która została skopiowana z hello portalu Azure do hello **adres URL wylogowania dostawcy identyfikator** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9b052-189">Paste **Sign-Out URL** value, which you have copied from hello Azure portal into hello **ID Provider Logout URL** textbox.</span></span>
    
     <span data-ttu-id="9b052-190">c.</span><span class="sxs-lookup"><span data-stu-id="9b052-190">c.</span></span> <span data-ttu-id="9b052-191">Otwieranie certyfikatu zakodowanego base-64 w Notatniku hello kopiowania zawartości go do Schowka, a następnie wklej go toohello **certyfikat dostawcy identyfikator** pole tekstowe</span><span class="sxs-lookup"><span data-stu-id="9b052-191">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **ID Provider Certificate** textbox</span></span>
     
     <span data-ttu-id="9b052-192">d.</span><span class="sxs-lookup"><span data-stu-id="9b052-192">d.</span></span> <span data-ttu-id="9b052-193">Witaj tooopen **ustawienia** kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="9b052-193">tooopen hello **Settings** page, click **Save**.</span></span>

12. <span data-ttu-id="9b052-194">Na powitania **ustawienia** kliknij przycisk **generowania tokenu rejestracji Jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="9b052-194">On hello **Settings** page, click **Generate SSO Token**.</span></span>

    <span data-ttu-id="9b052-195">![Ustawienia](./media/active-directory-saas-druva-tutorial/ic795093.png "ustawienia")</span><span class="sxs-lookup"><span data-stu-id="9b052-195">![Settings](./media/active-directory-saas-druva-tutorial/ic795093.png "Settings")</span></span>

13. <span data-ttu-id="9b052-196">Na powitania **pojedynczego logowania jednokrotnego tokenu uwierzytelniania** okna dialogowego, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9b052-196">On hello **Single Sign-on Authentication Token** dialog, perform hello following steps:</span></span>

    <span data-ttu-id="9b052-197">![Token rejestracji Jednokrotnej](./media/active-directory-saas-druva-tutorial/ic795094.png "tokenu rejestracji Jednokrotnej")</span><span class="sxs-lookup"><span data-stu-id="9b052-197">![SSO Token](./media/active-directory-saas-druva-tutorial/ic795094.png "SSO Token")</span></span>
    
    <span data-ttu-id="9b052-198">a.</span><span class="sxs-lookup"><span data-stu-id="9b052-198">a.</span></span> <span data-ttu-id="9b052-199">Kliknij przycisk **kopiowania**, wklej skopiowane wartość hello **wartość** textbox w hello **Dodawanie atrybutu** sekcji.</span><span class="sxs-lookup"><span data-stu-id="9b052-199">Click **Copy**, Paste copied value in hello **Value** textbox in hello **Add Attribute** section.</span></span>
    
    <span data-ttu-id="9b052-200">b.</span><span class="sxs-lookup"><span data-stu-id="9b052-200">b.</span></span> <span data-ttu-id="9b052-201">Kliknij przycisk **Zamknij**.</span><span class="sxs-lookup"><span data-stu-id="9b052-201">Click **Close**.</span></span>

> [!TIP]
> <span data-ttu-id="9b052-202">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="9b052-202">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9b052-203">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="9b052-203">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9b052-204">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9b052-204">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="9b052-205">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b052-205">Create an Azure AD test user</span></span>

<span data-ttu-id="9b052-206">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="9b052-206">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="9b052-208">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9b052-208">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b052-209">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9b052-209">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-druva-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="9b052-211">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="9b052-211">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-druva-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="9b052-213">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="9b052-213">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![przycisk Dodaj Hello](./media/active-directory-saas-druva-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="9b052-215">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9b052-215">In hello **User** dialog box, perform hello following steps:</span></span>

    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-druva-tutorial/create_aaduser_04.png)

    <span data-ttu-id="9b052-217">a.</span><span class="sxs-lookup"><span data-stu-id="9b052-217">a.</span></span> <span data-ttu-id="9b052-218">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9b052-218">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9b052-219">b.</span><span class="sxs-lookup"><span data-stu-id="9b052-219">b.</span></span> <span data-ttu-id="9b052-220">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9b052-220">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="9b052-221">c.</span><span class="sxs-lookup"><span data-stu-id="9b052-221">c.</span></span> <span data-ttu-id="9b052-222">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="9b052-222">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="9b052-223">d.</span><span class="sxs-lookup"><span data-stu-id="9b052-223">d.</span></span> <span data-ttu-id="9b052-224">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9b052-224">Click **Create**.</span></span>
 
### <a name="create-a-druva-test-user"></a><span data-ttu-id="9b052-225">Tworzenie użytkownika testowego Druva</span><span class="sxs-lookup"><span data-stu-id="9b052-225">Create a Druva test user</span></span>

<span data-ttu-id="9b052-226">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable w tooDruva muszą mieć przydzielone do Druva.</span><span class="sxs-lookup"><span data-stu-id="9b052-226">In order tooenable Azure AD users toolog in tooDruva, they must be provisioned into Druva.</span></span> <span data-ttu-id="9b052-227">W przypadku hello Druva Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="9b052-227">In hello case of Druva, provisioning is a manual task.</span></span>

<span data-ttu-id="9b052-228">**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9b052-228">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b052-229">Zaloguj się za tooyour **Druva** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="9b052-229">Log in tooyour **Druva** company site as administrator.</span></span>

2. <span data-ttu-id="9b052-230">Przejdź za**Zarządzaj \> użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="9b052-230">Go too**Manage \> Users**.</span></span>
   
   <span data-ttu-id="9b052-231">![Zarządzaj użytkownikami](./media/active-directory-saas-druva-tutorial/ic795097.png "Zarządzanie użytkownikami")</span><span class="sxs-lookup"><span data-stu-id="9b052-231">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795097.png "Manage Users")</span></span>

3. <span data-ttu-id="9b052-232">Kliknij przycisk **tworzenia nowych**.</span><span class="sxs-lookup"><span data-stu-id="9b052-232">Click **Create New**.</span></span>
   
   <span data-ttu-id="9b052-233">![Zarządzaj użytkownikami](./media/active-directory-saas-druva-tutorial/ic795098.png "Zarządzanie użytkownikami")</span><span class="sxs-lookup"><span data-stu-id="9b052-233">![Manage Users](./media/active-directory-saas-druva-tutorial/ic795098.png "Manage Users")</span></span>

4. <span data-ttu-id="9b052-234">W oknie dialogowym Tworzenie nowego użytkownika hello wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9b052-234">On hello Create New User dialog, perform hello following steps:</span></span>
   
   <span data-ttu-id="9b052-235">![Utwórz NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "utworzyć NewUser")</span><span class="sxs-lookup"><span data-stu-id="9b052-235">![Create NewUser](./media/active-directory-saas-druva-tutorial/ic795099.png "Create NewUser")</span></span>
   
   <span data-ttu-id="9b052-236">a.</span><span class="sxs-lookup"><span data-stu-id="9b052-236">a.</span></span> <span data-ttu-id="9b052-237">W hello **adres E-mail** pole tekstowe, wprowadź adres e-mail użytkownika, takie jak hello  **brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="9b052-237">In hello **Email address** textbox, enter hello email of user like **brittasimon@contoso.com**.</span></span>
   
   <span data-ttu-id="9b052-238">b.</span><span class="sxs-lookup"><span data-stu-id="9b052-238">b.</span></span> <span data-ttu-id="9b052-239">W hello **nazwa** pole tekstowe, wprowadź nazwę użytkownika, takie jak hello **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9b052-239">In hello **Name** textbox, enter hello name of user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="9b052-240">c.</span><span class="sxs-lookup"><span data-stu-id="9b052-240">c.</span></span> <span data-ttu-id="9b052-241">Kliknij przycisk **Utwórz użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="9b052-241">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="9b052-242">Możesz użyć innych Druva użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Druva tooprovision kont użytkowników usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b052-242">You can use any other Druva user account creation tools or APIs provided by Druva tooprovision Azure AD user accounts.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="9b052-243">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b052-243">Assign hello Azure AD test user</span></span>

<span data-ttu-id="9b052-244">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooDruva.</span><span class="sxs-lookup"><span data-stu-id="9b052-244">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDruva.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="9b052-246">**tooassign tooDruva Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="9b052-246">**tooassign Britta Simon tooDruva, perform hello following steps:**</span></span>

1. <span data-ttu-id="9b052-247">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9b052-247">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="9b052-249">Z listy aplikacji hello wybierz **Druva**.</span><span class="sxs-lookup"><span data-stu-id="9b052-249">In hello applications list, select **Druva**.</span></span>

    ![łącze Druva Hello na liście aplikacji hello](./media/active-directory-saas-druva-tutorial/tutorial_druva_app.png)  

3. <span data-ttu-id="9b052-251">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="9b052-251">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="9b052-253">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9b052-253">Click **Add** button.</span></span> <span data-ttu-id="9b052-254">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9b052-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="9b052-256">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9b052-256">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9b052-257">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9b052-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9b052-258">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9b052-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="9b052-259">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9b052-259">Test single sign-on</span></span>

<span data-ttu-id="9b052-260">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9b052-260">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9b052-261">Po kliknięciu kafelka Druva hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Druva aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9b052-261">When you click hello Druva tile in hello Access Panel, you should get automatically signed-on tooyour Druva application.</span></span>
<span data-ttu-id="9b052-262">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9b052-262">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="9b052-263">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9b052-263">Additional resources</span></span>

* [<span data-ttu-id="9b052-264">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b052-264">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9b052-265">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9b052-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-druva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-druva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-druva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-druva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-druva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-druva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-druva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-druva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-druva-tutorial/tutorial_general_203.png

