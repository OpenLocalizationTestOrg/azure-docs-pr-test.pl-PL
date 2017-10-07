---
title: 'Samouczek: Integracji Azure Active Directory z Learningpool Act | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między ustawa Learningpool i Azure Active Directory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 51e8695f-31e1-4d09-8eb3-13241999d99f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: f343623f08bb60e143aaff07d93e4ef773232e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learningpool-act"></a><span data-ttu-id="8ebb6-103">Samouczek: Integracji Azure Active Directory z Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="8ebb6-103">Tutorial: Azure Active Directory integration with Learningpool Act</span></span>

<span data-ttu-id="8ebb6-104">Z tego samouczka, dowiesz się, jak toointegrate Learningpool działają z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8ebb6-104">In this tutorial, you learn how toointegrate Learningpool Act with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8ebb6-105">Integracja z usługą Azure AD Learningpool Act zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8ebb6-105">Integrating Learningpool Act with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8ebb6-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooLearningpool Act</span><span class="sxs-lookup"><span data-stu-id="8ebb6-106">You can control in Azure AD who has access tooLearningpool Act</span></span>
- <span data-ttu-id="8ebb6-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooLearningpool Act (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ebb6-107">You can enable your users tooautomatically get signed-on tooLearningpool Act (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8ebb6-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8ebb6-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8ebb6-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8ebb6-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ebb6-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8ebb6-110">Prerequisites</span></span>

<span data-ttu-id="8ebb6-111">tooconfigure integracji usługi Azure AD z Learningpool Act, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8ebb6-111">tooconfigure Azure AD integration with Learningpool Act, you need hello following items:</span></span>

- <span data-ttu-id="8ebb6-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ebb6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8ebb6-113">Działanie Learningpool logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8ebb6-113">A Learningpool Act single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8ebb6-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8ebb6-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8ebb6-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8ebb6-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8ebb6-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ebb6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8ebb6-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8ebb6-118">Scenario description</span></span>
<span data-ttu-id="8ebb6-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8ebb6-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8ebb6-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8ebb6-121">Dodawanie z galerii hello Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="8ebb6-121">Adding Learningpool Act from hello gallery</span></span>
2. <span data-ttu-id="8ebb6-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8ebb6-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learningpool-act-from-hello-gallery"></a><span data-ttu-id="8ebb6-123">Dodawanie z galerii hello Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="8ebb6-123">Adding Learningpool Act from hello gallery</span></span>
<span data-ttu-id="8ebb6-124">tooconfigure hello integracji Learningpool Act do usługi Azure AD, należy tooadd Learningpool Act z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-124">tooconfigure hello integration of Learningpool Act into Azure AD, you need tooadd Learningpool Act from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8ebb6-125">**tooadd Learningpool Act z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="8ebb6-125">**tooadd Learningpool Act from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ebb6-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="8ebb6-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8ebb6-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="8ebb6-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="8ebb6-133">W polu wyszukiwania hello wpisz **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-133">In hello search box, type **Learningpool Act**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_search.png)

5. <span data-ttu-id="8ebb6-135">W panelu wyników hello, wybierz **Learningpool Act**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-135">In hello results panel, select **Learningpool Act**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8ebb6-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8ebb6-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8ebb6-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z Learningpool Act w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-138">In this section, you configure and test Azure AD single sign-on with Learningpool Act based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="8ebb6-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello ustawy Learningpool jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Learningpool Act is tooa user in Azure AD.</span></span> <span data-ttu-id="8ebb6-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi ustawy Learningpool musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-140">In other words, a link relationship between an Azure AD user and hello related user in Learningpool Act needs toobe established.</span></span>

<span data-ttu-id="8ebb6-141">W Learningpool Act, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-141">In Learningpool Act, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="8ebb6-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Learningpool Act, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8ebb6-142">tooconfigure and test Azure AD single sign-on with Learningpool Act, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8ebb6-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8ebb6-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8ebb6-145">**[Tworzenie użytkownika testowego Learningpool Act](#creating-a-learningpool-act-test-user)**  -toohave odpowiednikiem Simona Britta w Learningpool Act, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-145">**[Creating a Learningpool Act test user](#creating-a-learningpool-act-test-user)** - toohave a counterpart of Britta Simon in Learningpool Act that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="8ebb6-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8ebb6-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8ebb6-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8ebb6-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8ebb6-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Learningpool Act application.</span></span>

<span data-ttu-id="8ebb6-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Learningpool Act, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8ebb6-150">**tooconfigure Azure AD single sign-on with Learningpool Act, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ebb6-151">W portalu Azure na powitania hello **Learningpool Act** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-151">In hello Azure portal, on hello **Learningpool Act** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="8ebb6-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_samlbase.png)

3. <span data-ttu-id="8ebb6-155">Na powitania **Learningpool Act domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8ebb6-155">On hello **Learningpool Act Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_url.png)

    <span data-ttu-id="8ebb6-157">a.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-157">a.</span></span> <span data-ttu-id="8ebb6-158">W hello **adres URL logowania** pole tekstowe, wprowadź adres URL hello:`https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span><span class="sxs-lookup"><span data-stu-id="8ebb6-158">In hello **Sign-on URL** textbox, type hello URL: `https://parliament.preview.Learningpool.com/auth/shibboleth/index.php`</span></span>

    <span data-ttu-id="8ebb6-159">b.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-159">b.</span></span> <span data-ttu-id="8ebb6-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="8ebb6-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<subdomain>.Learningpool.com/shibboleth` |
    | `https://<subdomain>.preview.Learningpool.com/shibboleth` |

    > [!NOTE] 
    > <span data-ttu-id="8ebb6-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-161">These values are not real.</span></span> <span data-ttu-id="8ebb6-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="8ebb6-163">Skontaktuj się z [zespołem pomocy technicznej klienta Act Learningpool](https://www.Learningpool.com/support) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-163">Contact [Learningpool Act Client support team](https://www.Learningpool.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="8ebb6-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_certificate.png) 

5. <span data-ttu-id="8ebb6-166">Stosowanie ustawy Learningpool oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-166">Learningpool Act application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="8ebb6-167">Skonfiguruj powitania po oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-167">Please configure hello following claims for this application.</span></span> <span data-ttu-id="8ebb6-168">Można zarządzać hello wartości tych atrybutów z hello **"Atrribute"** kartę aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-168">You can manage hello values of these attributes from hello **"Atrribute"** tab of hello application.</span></span> <span data-ttu-id="8ebb6-169">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-169">hello following screenshot shows an example for this.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_attribute.png) 

6. <span data-ttu-id="8ebb6-171">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie hello i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8ebb6-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="8ebb6-172">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="8ebb6-172">Attribute Name</span></span> | <span data-ttu-id="8ebb6-173">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="8ebb6-173">Attribute Value</span></span> |
    | ------------------- | -------------------- |
    | <span data-ttu-id="8ebb6-174">urn: oid:1.2.840.113556.1.4.221</span><span class="sxs-lookup"><span data-stu-id="8ebb6-174">urn:oid:1.2.840.113556.1.4.221</span></span> | <span data-ttu-id="8ebb6-175">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="8ebb6-175">user.userprincipalname</span></span> |
    | <span data-ttu-id="8ebb6-176">urn: oid:2.5.4.42</span><span class="sxs-lookup"><span data-stu-id="8ebb6-176">urn:oid:2.5.4.42</span></span> | <span data-ttu-id="8ebb6-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="8ebb6-177">user.givenname</span></span> |
    | <span data-ttu-id="8ebb6-178">urn: oid:0.9.2342.19200300.100.1.3</span><span class="sxs-lookup"><span data-stu-id="8ebb6-178">urn:oid:0.9.2342.19200300.100.1.3</span></span> | <span data-ttu-id="8ebb6-179">User.mail</span><span class="sxs-lookup"><span data-stu-id="8ebb6-179">user.mail</span></span> |    
    | <span data-ttu-id="8ebb6-180">urn: oid:2.5.4.4</span><span class="sxs-lookup"><span data-stu-id="8ebb6-180">urn:oid:2.5.4.4</span></span> | <span data-ttu-id="8ebb6-181">User.surname</span><span class="sxs-lookup"><span data-stu-id="8ebb6-181">user.surname</span></span> |
    
    <span data-ttu-id="8ebb6-182">a.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-182">a.</span></span> <span data-ttu-id="8ebb6-183">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-183">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Learningpool-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="8ebb6-186">b.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-186">b.</span></span> <span data-ttu-id="8ebb6-187">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-187">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="8ebb6-188">c.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-188">c.</span></span> <span data-ttu-id="8ebb6-189">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-189">From hello **Value** list, type hello attribute value shown for that row.</span></span>

    <span data-ttu-id="8ebb6-190">d.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-190">d.</span></span> <span data-ttu-id="8ebb6-191">Pozostaw hello **Namespace** puste.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-191">Leave hello **Namespace** blank.</span></span>
    
    <span data-ttu-id="8ebb6-192">e.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-192">e.</span></span> <span data-ttu-id="8ebb6-193">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-193">Click **Ok**.</span></span>

7. <span data-ttu-id="8ebb6-194">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-194">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Learningpool-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="8ebb6-196">tooconfigure rejestracji jednokrotnej w **Learningpool Act** strony, należy pobrać hello toosend **XML metadanych** za[zespołem pomocy technicznej Learningpool Act](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="8ebb6-196">tooconfigure single sign-on on **Learningpool Act** side, you need toosend hello downloaded **Metadata XML** too[Learningpool Act support team](https://www.Learningpool.com/support).</span></span> <span data-ttu-id="8ebb6-197">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-197">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="8ebb6-198">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="8ebb6-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8ebb6-199">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8ebb6-200">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8ebb6-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8ebb6-201">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ebb6-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="8ebb6-202">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="8ebb6-204">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8ebb6-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ebb6-205">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8ebb6-207">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8ebb6-209">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8ebb6-211">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8ebb6-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-Learningpool-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8ebb6-213">a.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-213">a.</span></span> <span data-ttu-id="8ebb6-214">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8ebb6-215">b.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-215">b.</span></span> <span data-ttu-id="8ebb6-216">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8ebb6-217">c.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-217">c.</span></span> <span data-ttu-id="8ebb6-218">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8ebb6-219">d.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-219">d.</span></span> <span data-ttu-id="8ebb6-220">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-220">Click **Create**.</span></span>
 
### <a name="creating-a-learningpool-act-test-user"></a><span data-ttu-id="8ebb6-221">Tworzenie użytkownika testowego Learningpool Act</span><span class="sxs-lookup"><span data-stu-id="8ebb6-221">Creating a Learningpool Act test user</span></span>

<span data-ttu-id="8ebb6-222">toolog użytkowników tooenable usługi Azure AD w tooLearningpool Act, muszą mieć przydzielone do Learningpool Act.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-222">tooenable Azure AD users toolog in tooLearningpool Act, they must be provisioned into Learningpool Act.</span></span>

<span data-ttu-id="8ebb6-223">Nie ma elementu akcji można tooconfigure użytkownika inicjowania obsługi administracyjnej tooLearningpool Act.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-223">There is no action item for you tooconfigure user provisioning tooLearningpool Act.</span></span>  
<span data-ttu-id="8ebb6-224">Użytkownicy muszą toobe utworzone przez użytkownika [zespołem pomocy technicznej Learningpool Act](https://www.Learningpool.com/support).</span><span class="sxs-lookup"><span data-stu-id="8ebb6-224">Users need toobe created by your [Learningpool Act support team](https://www.Learningpool.com/support).</span></span>

>[!NOTE]
><span data-ttu-id="8ebb6-225">Możesz użyć innych Learningpool Act użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez działanie Learningpool tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-225">You can use any other Learningpool Act user account creation tools or APIs provided by Learningpool Act tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8ebb6-226">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ebb6-226">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8ebb6-227">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooLearningpool działanie.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-227">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLearningpool Act.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="8ebb6-229">**tooassign tooLearningpool Simona Britta Act, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="8ebb6-229">**tooassign Britta Simon tooLearningpool Act, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ebb6-230">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-230">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8ebb6-232">Z listy aplikacji hello wybierz **Learningpool Act**.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-232">In hello applications list, select **Learningpool Act**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-Learningpool-tutorial/tutorial_Learningpoolact_app.png) 

3. <span data-ttu-id="8ebb6-234">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-234">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="8ebb6-236">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-236">Click **Add** button.</span></span> <span data-ttu-id="8ebb6-237">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="8ebb6-239">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-239">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8ebb6-240">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8ebb6-241">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8ebb6-242">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8ebb6-242">Testing single sign-on</span></span>

<span data-ttu-id="8ebb6-243">Celem Hello w tej sekcji jest tootest użyciu usługi Azure AD konfiguracji rejestracji jednokrotnej hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-243">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8ebb6-244">Po kliknięciu hello Learningpool Act kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Learningpool działanie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ebb6-244">When you click hello Learningpool Act tile in hello Access Panel, you should get automatically signed-on tooyour Learningpool Act application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8ebb6-245">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8ebb6-245">Additional resources</span></span>

* [<span data-ttu-id="8ebb6-246">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ebb6-246">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8ebb6-247">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8ebb6-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-Learningpool-tutorial/tutorial_general_203.png

