---
title: 'Samouczek: Integracji Azure Active Directory z Klue | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Klue."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 08341008-980b-4111-adb2-97bbabbf1e47
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: bb9134a558d6c050f428690d57a3cea850b7dbee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-klue"></a><span data-ttu-id="008f1-103">Samouczek: Integracji Azure Active Directory z Klue</span><span class="sxs-lookup"><span data-stu-id="008f1-103">Tutorial: Azure Active Directory integration with Klue</span></span>

<span data-ttu-id="008f1-104">Z tego samouczka, dowiesz się, jak toointegrate Klue w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="008f1-104">In this tutorial, you learn how toointegrate Klue with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="008f1-105">Integracja z usługą Azure AD Klue zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="008f1-105">Integrating Klue with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="008f1-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooKlue</span><span class="sxs-lookup"><span data-stu-id="008f1-106">You can control in Azure AD who has access tooKlue</span></span>
- <span data-ttu-id="008f1-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooKlue (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="008f1-107">You can enable your users tooautomatically get signed-on tooKlue (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="008f1-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="008f1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="008f1-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="008f1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="008f1-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="008f1-110">Prerequisites</span></span>

<span data-ttu-id="008f1-111">tooconfigure integracji z usługą Azure AD z Klue należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="008f1-111">tooconfigure Azure AD integration with Klue, you need hello following items:</span></span>

- <span data-ttu-id="008f1-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="008f1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="008f1-113">Klue logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="008f1-113">A Klue single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="008f1-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="008f1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="008f1-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="008f1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="008f1-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="008f1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="008f1-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="008f1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="008f1-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="008f1-118">Scenario description</span></span>
<span data-ttu-id="008f1-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="008f1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="008f1-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="008f1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="008f1-121">Dodawanie Klue z galerii hello</span><span class="sxs-lookup"><span data-stu-id="008f1-121">Adding Klue from hello gallery</span></span>
2. <span data-ttu-id="008f1-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="008f1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-klue-from-hello-gallery"></a><span data-ttu-id="008f1-123">Dodawanie Klue z galerii hello</span><span class="sxs-lookup"><span data-stu-id="008f1-123">Adding Klue from hello gallery</span></span>
<span data-ttu-id="008f1-124">tooconfigure hello integracji Klue do usługi Azure AD, należy tooadd Klue z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="008f1-124">tooconfigure hello integration of Klue into Azure AD, you need tooadd Klue from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="008f1-125">**tooadd Klue z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="008f1-125">**tooadd Klue from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="008f1-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="008f1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="008f1-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="008f1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="008f1-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="008f1-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="008f1-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="008f1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="008f1-133">W polu wyszukiwania hello wpisz **Klue**.</span><span class="sxs-lookup"><span data-stu-id="008f1-133">In hello search box, type **Klue**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-klue-tutorial/tutorial_klue_search.png)

5. <span data-ttu-id="008f1-135">W panelu wyników hello zaznacz **Klue**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="008f1-135">In hello results panel, select **Klue**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-klue-tutorial/tutorial_klue_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="008f1-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="008f1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="008f1-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Klue w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="008f1-138">In this section, you configure and test Azure AD single sign-on with Klue based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="008f1-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Klue jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="008f1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Klue is tooa user in Azure AD.</span></span> <span data-ttu-id="008f1-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Klue musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="008f1-140">In other words, a link relationship between an Azure AD user and hello related user in Klue needs toobe established.</span></span>

<span data-ttu-id="008f1-141">W Klue, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="008f1-141">In Klue, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="008f1-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Klue, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="008f1-142">tooconfigure and test Azure AD single sign-on with Klue, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="008f1-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="008f1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="008f1-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="008f1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="008f1-145">**[Tworzenie użytkownika testowego Klue](#creating-a-klue-test-user)**  -toohave odpowiednikiem Simona Britta w Klue, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="008f1-145">**[Creating a Klue test user](#creating-a-klue-test-user)** - toohave a counterpart of Britta Simon in Klue that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="008f1-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="008f1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="008f1-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="008f1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="008f1-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="008f1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="008f1-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Klue.</span><span class="sxs-lookup"><span data-stu-id="008f1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Klue application.</span></span>

<span data-ttu-id="008f1-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Klue, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="008f1-150">**tooconfigure Azure AD single sign-on with Klue, perform hello following steps:**</span></span>

1. <span data-ttu-id="008f1-151">W portalu Azure na powitania hello **Klue** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="008f1-151">In hello Azure portal, on hello **Klue** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="008f1-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="008f1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-klue-tutorial/tutorial_klue_samlbase.png)

3. <span data-ttu-id="008f1-155">Na powitania **Klue domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="008f1-155">On hello **Klue Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-klue-tutorial/tutorial_klue_url1.png)

    <span data-ttu-id="008f1-157">a.</span><span class="sxs-lookup"><span data-stu-id="008f1-157">a.</span></span> <span data-ttu-id="008f1-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`urn:klue:<Customer ID>`</span><span class="sxs-lookup"><span data-stu-id="008f1-158">In hello **Identifier** textbox, type a URL using hello following pattern: `urn:klue:<Customer ID>`</span></span>

    <span data-ttu-id="008f1-159">b.</span><span class="sxs-lookup"><span data-stu-id="008f1-159">b.</span></span> <span data-ttu-id="008f1-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span><span class="sxs-lookup"><span data-stu-id="008f1-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/callback`</span></span>

4. <span data-ttu-id="008f1-161">Sprawdź **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="008f1-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="008f1-162">Jeśli chcesz, aby aplikacja hello tooconfigure w **SP** inicjowane tryb:</span><span class="sxs-lookup"><span data-stu-id="008f1-162">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-klue-tutorial/tutorial_klue_url2.png)

    <span data-ttu-id="008f1-164">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://app.klue.com/account/auth/saml/<Customer UUID>/`</span><span class="sxs-lookup"><span data-stu-id="008f1-164">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://app.klue.com/account/auth/saml/<Customer UUID>/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="008f1-165">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="008f1-165">These values are not real.</span></span> <span data-ttu-id="008f1-166">Witaj rzeczywisty adres URL odpowiedzi służący, identyfikator i adres URL logowania, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="008f1-166">Update these values with hello actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="008f1-167">Skontaktuj się z [zespołem pomocy technicznej klienta Klue](mailto:support@klue.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="008f1-167">Contact [Klue Client support team](mailto:support@klue.com) tooget these values.</span></span>

5. <span data-ttu-id="008f1-168">Witaj Klue aplikacji oczekuje potwierdzenia SAML hello w określonym formacie wymaga możesz tooadd atrybutu niestandardowego mapowania tooyour SAML tokenu atrybuty konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="008f1-168">hello Klue application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="008f1-169">Można zarządzać hello wartości tych atrybutów z hello "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="008f1-169">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-klue-tutorial/attribute.png)

6. <span data-ttu-id="008f1-171">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, Konfigurowanie atrybutu tokenu SAML, jak pokazano w hello poprzedzających obrazu i wykonywanie hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="008f1-171">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello preceding image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="008f1-172">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="008f1-172">Attribute Name</span></span>      | <span data-ttu-id="008f1-173">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="008f1-173">Attribute Value</span></span>      |
    | ------------------- | -------------------- |
    | <span data-ttu-id="008f1-174">Imię</span><span class="sxs-lookup"><span data-stu-id="008f1-174">first_name</span></span>          | <span data-ttu-id="008f1-175">User.givenName</span><span class="sxs-lookup"><span data-stu-id="008f1-175">user.givenname</span></span> |
    | <span data-ttu-id="008f1-176">nazwisko</span><span class="sxs-lookup"><span data-stu-id="008f1-176">last_name</span></span>           | <span data-ttu-id="008f1-177">User.surname</span><span class="sxs-lookup"><span data-stu-id="008f1-177">user.surname</span></span> |
    | <span data-ttu-id="008f1-178">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="008f1-178">email</span></span>               | <span data-ttu-id="008f1-179">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="008f1-179">user.userprincipalname</span></span>|
    
    <span data-ttu-id="008f1-180">a.</span><span class="sxs-lookup"><span data-stu-id="008f1-180">a.</span></span> <span data-ttu-id="008f1-181">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="008f1-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-klue-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-klue-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="008f1-184">b.</span><span class="sxs-lookup"><span data-stu-id="008f1-184">b.</span></span> <span data-ttu-id="008f1-185">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="008f1-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="008f1-186">c.</span><span class="sxs-lookup"><span data-stu-id="008f1-186">c.</span></span> <span data-ttu-id="008f1-187">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="008f1-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="008f1-188">d.</span><span class="sxs-lookup"><span data-stu-id="008f1-188">d.</span></span> <span data-ttu-id="008f1-189">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="008f1-189">Click **Ok**.</span></span>

7. <span data-ttu-id="008f1-190">Na powitania **certyfikat podpisywania SAML** kliknij **Certificate(Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="008f1-190">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-klue-tutorial/tutorial_klue_certificate.png) 

8. <span data-ttu-id="008f1-192">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="008f1-192">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-klue-tutorial/tutorial_general_400.png)
    
9. <span data-ttu-id="008f1-194">Na powitania **konfiguracji Klue** kliknij **skonfigurować Klue** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="008f1-194">On hello **Klue Configuration** section, click **Configure Klue** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="008f1-195">Kopiuj hello **identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="008f1-195">Copy hello **SAML Entity ID and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-klue-tutorial/tutorial_klue_configure.png) 

10. <span data-ttu-id="008f1-197">tooconfigure rejestracji jednokrotnej w **Klue** strony, należy pobrać hello toosend **Certificate(Base64) SAML pojedynczy znak na adres URL usługi i identyfikator jednostki SAML** zbyt[zespołem pomocy technicznej Klue](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="008f1-197">tooconfigure single sign-on on **Klue** side, you need toosend hello downloaded **Certificate(Base64), SAML Single Sign-On Service URL, and SAML Entity ID** too[Klue support team](mailto:support@klue.com).</span></span>

> [!TIP]
> <span data-ttu-id="008f1-198">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="008f1-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="008f1-199">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="008f1-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="008f1-200">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="008f1-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="008f1-201">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="008f1-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="008f1-202">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="008f1-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="008f1-204">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="008f1-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="008f1-205">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="008f1-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="008f1-207">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="008f1-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="008f1-209">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="008f1-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="008f1-211">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="008f1-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-klue-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="008f1-213">a.</span><span class="sxs-lookup"><span data-stu-id="008f1-213">a.</span></span> <span data-ttu-id="008f1-214">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="008f1-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="008f1-215">b.</span><span class="sxs-lookup"><span data-stu-id="008f1-215">b.</span></span> <span data-ttu-id="008f1-216">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="008f1-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="008f1-217">c.</span><span class="sxs-lookup"><span data-stu-id="008f1-217">c.</span></span> <span data-ttu-id="008f1-218">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="008f1-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="008f1-219">d.</span><span class="sxs-lookup"><span data-stu-id="008f1-219">d.</span></span> <span data-ttu-id="008f1-220">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="008f1-220">Click **Create**.</span></span>
 
### <a name="creating-a-klue-test-user"></a><span data-ttu-id="008f1-221">Tworzenie użytkownika testowego Klue</span><span class="sxs-lookup"><span data-stu-id="008f1-221">Creating a Klue test user</span></span>

<span data-ttu-id="008f1-222">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w Klue.</span><span class="sxs-lookup"><span data-stu-id="008f1-222">hello objective of this section is toocreate a user called Britta Simon in Klue.</span></span> <span data-ttu-id="008f1-223">Klue obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="008f1-223">Klue supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="008f1-224">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="008f1-224">There is no action item for you in this section.</span></span> <span data-ttu-id="008f1-225">Nowy użytkownik jest tworzona podczas próby tooaccess Klue, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="008f1-225">A new user is created during an attempt tooaccess Klue if it doesn't exist yet.</span></span>

>[!Note]
><span data-ttu-id="008f1-226">Jeśli potrzebujesz toocreate użytkownik ręcznie, skontaktuj się z [zespołem pomocy technicznej Klue](mailto:support@klue.com).</span><span class="sxs-lookup"><span data-stu-id="008f1-226">If you need toocreate a user manually, Contact [Klue support team](mailto:support@klue.com).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="008f1-227">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="008f1-227">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="008f1-228">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooKlue.</span><span class="sxs-lookup"><span data-stu-id="008f1-228">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKlue.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="008f1-230">**tooassign tooKlue Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="008f1-230">**tooassign Britta Simon tooKlue, perform hello following steps:**</span></span>

1. <span data-ttu-id="008f1-231">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="008f1-231">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="008f1-233">Z listy aplikacji hello wybierz **Klue**.</span><span class="sxs-lookup"><span data-stu-id="008f1-233">In hello applications list, select **Klue**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-klue-tutorial/tutorial_klue_app.png) 

3. <span data-ttu-id="008f1-235">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="008f1-235">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="008f1-237">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="008f1-237">Click **Add** button.</span></span> <span data-ttu-id="008f1-238">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="008f1-238">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="008f1-240">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="008f1-240">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="008f1-241">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="008f1-241">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="008f1-242">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="008f1-242">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="008f1-243">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="008f1-243">Testing single sign-on</span></span>

<span data-ttu-id="008f1-244">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="008f1-244">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="008f1-245">Po kliknięciu kafelka Klue hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Klue aplikacji.</span><span class="sxs-lookup"><span data-stu-id="008f1-245">When you click hello Klue tile in hello Access Panel, you should get automatically signed-on tooyour Klue application.</span></span>
<span data-ttu-id="008f1-246">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="008f1-246">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="008f1-247">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="008f1-247">Additional resources</span></span>

* [<span data-ttu-id="008f1-248">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="008f1-248">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="008f1-249">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="008f1-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-klue-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-klue-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-klue-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-klue-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-klue-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-klue-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-klue-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-klue-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-klue-tutorial/tutorial_general_203.png

