---
title: 'Samouczek: Integracji Azure Active Directory z Trello | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Trello."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cd5ae365-9ed6-43a6-920b-f7814b993949
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: jeedes
ms.openlocfilehash: de2f2ba6a0e5545983c351f26f99d14f436618c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-trello"></a><span data-ttu-id="49c4a-103">Samouczek: Integracji Azure Active Directory z Trello</span><span class="sxs-lookup"><span data-stu-id="49c4a-103">Tutorial: Azure Active Directory integration with Trello</span></span>

<span data-ttu-id="49c4a-104">Z tego samouczka, dowiesz się, jak toointegrate Trello w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="49c4a-104">In this tutorial, you learn how toointegrate Trello with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="49c4a-105">Integracja z usługą Azure AD Trello zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="49c4a-105">Integrating Trello with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="49c4a-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooTrello</span><span class="sxs-lookup"><span data-stu-id="49c4a-106">You can control in Azure AD who has access tooTrello</span></span>
- <span data-ttu-id="49c4a-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooTrello (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="49c4a-107">You can enable your users tooautomatically get signed-on tooTrello (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="49c4a-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="49c4a-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="49c4a-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="49c4a-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49c4a-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="49c4a-110">Prerequisites</span></span>

<span data-ttu-id="49c4a-111">tooconfigure integracji z usługą Azure AD z Trello należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="49c4a-111">tooconfigure Azure AD integration with Trello, you need hello following items:</span></span>

- <span data-ttu-id="49c4a-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="49c4a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="49c4a-113">Trello logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="49c4a-113">A Trello single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="49c4a-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="49c4a-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="49c4a-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="49c4a-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="49c4a-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="49c4a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="49c4a-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="49c4a-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="49c4a-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="49c4a-118">Scenario description</span></span>
<span data-ttu-id="49c4a-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="49c4a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="49c4a-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="49c4a-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="49c4a-121">Dodawanie Trello z galerii hello</span><span class="sxs-lookup"><span data-stu-id="49c4a-121">Adding Trello from hello gallery</span></span>
2. <span data-ttu-id="49c4a-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="49c4a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-trello-from-hello-gallery"></a><span data-ttu-id="49c4a-123">Dodawanie Trello z galerii hello</span><span class="sxs-lookup"><span data-stu-id="49c4a-123">Adding Trello from hello gallery</span></span>
<span data-ttu-id="49c4a-124">tooconfigure hello integracji Trello do usługi Azure AD, należy tooadd Trello z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="49c4a-124">tooconfigure hello integration of Trello into Azure AD, you need tooadd Trello from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="49c4a-125">**tooadd Trello z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="49c4a-125">**tooadd Trello from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="49c4a-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="49c4a-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="49c4a-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="49c4a-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="49c4a-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="49c4a-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="49c4a-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="49c4a-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="49c4a-133">W polu wyszukiwania hello wpisz **Trello**.</span><span class="sxs-lookup"><span data-stu-id="49c4a-133">In hello search box, type **Trello**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-trello-tutorial/tutorial_trello_search.png)

5. <span data-ttu-id="49c4a-135">W panelu wyników hello zaznacz **Trello**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="49c4a-135">In hello results panel, select **Trello**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-trello-tutorial/tutorial_trello_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="49c4a-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="49c4a-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="49c4a-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Trello w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="49c4a-138">In this section, you configure and test Azure AD single sign-on with Trello based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="49c4a-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Trello jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49c4a-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Trello is tooa user in Azure AD.</span></span> <span data-ttu-id="49c4a-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Trello musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="49c4a-140">In other words, a link relationship between an Azure AD user and hello related user in Trello needs toobe established.</span></span>

<span data-ttu-id="49c4a-141">W Trello, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="49c4a-141">In Trello, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="49c4a-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Trello, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="49c4a-142">tooconfigure and test Azure AD single sign-on with Trello, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="49c4a-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="49c4a-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="49c4a-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="49c4a-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="49c4a-145">**[Tworzenie użytkownika testowego Trello](#creating-a-trello-test-user)**  -toohave odpowiednikiem Simona Britta w Trello, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="49c4a-145">**[Creating a Trello test user](#creating-a-trello-test-user)** - toohave a counterpart of Britta Simon in Trello that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="49c4a-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="49c4a-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="49c4a-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="49c4a-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="49c4a-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="49c4a-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="49c4a-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji Trello.</span><span class="sxs-lookup"><span data-stu-id="49c4a-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Trello application.</span></span>

<span data-ttu-id="49c4a-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Trello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="49c4a-150">**tooconfigure Azure AD single sign-on with Trello, perform hello following steps:**</span></span>

1. <span data-ttu-id="49c4a-151">W portalu Azure na powitania hello **Trello** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="49c4a-151">In hello Azure portal, on hello **Trello** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="49c4a-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="49c4a-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trello-tutorial/tutorial_trello_samlbase.png)

3. <span data-ttu-id="49c4a-155">Na powitania **Trello domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP zainicjował tryb**, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="49c4a-155">On hello **Trello Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trello-tutorial/tutorial_trello_url.png)

    <span data-ttu-id="49c4a-157">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="49c4a-157">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

4. <span data-ttu-id="49c4a-158">Na powitania **Trello domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **SP zainicjował tryb**, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="49c4a-158">On hello **Trello Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trello-tutorial/tutorial_trello_url1.png)

    <span data-ttu-id="49c4a-160">a.</span><span class="sxs-lookup"><span data-stu-id="49c4a-160">a.</span></span> <span data-ttu-id="49c4a-161">Polecenie hello **Pokaż zaawansowane ustawienia adresu URL**.</span><span class="sxs-lookup"><span data-stu-id="49c4a-161">Click on hello **Show advanced URL settings**.</span></span>

    <span data-ttu-id="49c4a-162">b.</span><span class="sxs-lookup"><span data-stu-id="49c4a-162">b.</span></span> <span data-ttu-id="49c4a-163">W hello **na adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://trello.com/auth/saml/consume/<enterprise>`</span><span class="sxs-lookup"><span data-stu-id="49c4a-163">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://trello.com/auth/saml/consume/<enterprise>`</span></span>

    >[!NOTE]
    ><span data-ttu-id="49c4a-164">Należy pobrać hello  **\<enterprise\>**  informacji o pracy z Trello.</span><span class="sxs-lookup"><span data-stu-id="49c4a-164">You should get hello **\<enterprise\>** slug from Trello.</span></span> <span data-ttu-id="49c4a-165">Jeśli nie masz wartość sluga hello, skontaktuj się z [zespołem pomocy technicznej Trello](mailto:support@trello.com) tooget hello sluga dla przedsiębiorstwa należy.</span><span class="sxs-lookup"><span data-stu-id="49c4a-165">If you don't have hello slug value, contact [Trello support team](mailto:support@trello.com) tooget hello slug for you enterprise.</span></span>
    > 

5. <span data-ttu-id="49c4a-166">Aplikacja Trello oczekuje hello SAML potwierdzenia toocontain określonych atrybutów.</span><span class="sxs-lookup"><span data-stu-id="49c4a-166">Trello application expects hello SAML assertions toocontain specific attributes.</span></span> <span data-ttu-id="49c4a-167">Skonfiguruj hello następujące atrybuty dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="49c4a-167">Configure hello following attributes  for this application.</span></span> <span data-ttu-id="49c4a-168">Można zarządzać hello wartości tych atrybutów z hello **"Atrybuty użytkownika"** aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="49c4a-168">You can manage hello values of these attributes from hello **"User Attributes"** of hello application.</span></span> <span data-ttu-id="49c4a-169">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="49c4a-169">hello following screenshot shows an example for this.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trello-tutorial/tutorial_trello_attribute.png)

6. <span data-ttu-id="49c4a-171">Na powitania **atrybuty tokenu SAML** okna dialogowego, dla każdego wiersza przedstawione w poniższej tabeli hello wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="49c4a-171">On hello **SAML token attributes** dialog, for each row shown in hello table below, perform hello following steps:</span></span>
 
    | <span data-ttu-id="49c4a-172">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="49c4a-172">Attribute Name</span></span> | <span data-ttu-id="49c4a-173">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="49c4a-173">Attribute Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="49c4a-174">User.Email</span><span class="sxs-lookup"><span data-stu-id="49c4a-174">User.Email</span></span> | <span data-ttu-id="49c4a-175">User.mail</span><span class="sxs-lookup"><span data-stu-id="49c4a-175">user.mail</span></span> |
    | <span data-ttu-id="49c4a-176">User.FirstName</span><span class="sxs-lookup"><span data-stu-id="49c4a-176">User.FirstName</span></span> | <span data-ttu-id="49c4a-177">User.givenName</span><span class="sxs-lookup"><span data-stu-id="49c4a-177">user.givenname</span></span> |
    | <span data-ttu-id="49c4a-178">User.LastName</span><span class="sxs-lookup"><span data-stu-id="49c4a-178">User.LastName</span></span> | <span data-ttu-id="49c4a-179">User.surname</span><span class="sxs-lookup"><span data-stu-id="49c4a-179">user.surname</span></span> |

    <span data-ttu-id="49c4a-180">a.</span><span class="sxs-lookup"><span data-stu-id="49c4a-180">a.</span></span> <span data-ttu-id="49c4a-181">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="49c4a-181">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trello-tutorial/tutorial_officespace_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trello-tutorial/tutorial_officespace_05.png)

    <span data-ttu-id="49c4a-184">b.</span><span class="sxs-lookup"><span data-stu-id="49c4a-184">b.</span></span> <span data-ttu-id="49c4a-185">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="49c4a-185">In hello **Name** textbox, type hello attribute name shown for that row.</span></span> 

    <span data-ttu-id="49c4a-186">c.</span><span class="sxs-lookup"><span data-stu-id="49c4a-186">c.</span></span> <span data-ttu-id="49c4a-187">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="49c4a-187">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="49c4a-188">d.</span><span class="sxs-lookup"><span data-stu-id="49c4a-188">d.</span></span> <span data-ttu-id="49c4a-189">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="49c4a-189">Click **Ok**.</span></span> 
 
7. <span data-ttu-id="49c4a-190">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="49c4a-190">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trello-tutorial/tutorial_trello_certificate.png) 

8. <span data-ttu-id="49c4a-192">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="49c4a-192">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trello-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="49c4a-194">Na powitania **konfiguracji Trello** kliknij **skonfigurować Trello** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="49c4a-194">On hello **Trello Configuration** section, click **Configure Trello** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="49c4a-195">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="49c4a-195">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trello-tutorial/tutorial_trello_configure.png) 

9. <span data-ttu-id="49c4a-197">tooget logowania jednokrotnego skonfigurowane dla danej aplikacji, przejdź zbyt[konfiguracji logowania jednokrotnego przedsiębiorstwa Trello](https://trello.com/sso-configuration) toosend strony [zespołem pomocy technicznej Trello](mailto:support@trello.com) hello **SAML pojedynczy znak na adres URL usługi** i Dołącz hello **certyfikatu (Base64)**.</span><span class="sxs-lookup"><span data-stu-id="49c4a-197">tooget SSO configured for your application, go too[Trello enterprise SSO configuration](https://trello.com/sso-configuration) page toosend [Trello support team](mailto:support@trello.com) hello **SAML Single Sign-On Service URL** and attach hello **Certificate (Base64)**.</span></span>

> [!TIP]
> <span data-ttu-id="49c4a-198">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="49c4a-198">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="49c4a-199">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="49c4a-199">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="49c4a-200">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="49c4a-200">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="49c4a-201">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="49c4a-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="49c4a-202">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="49c4a-202">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="49c4a-204">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="49c4a-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="49c4a-205">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="49c4a-205">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="49c4a-207">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="49c4a-207">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="49c4a-209">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="49c4a-209">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="49c4a-211">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="49c4a-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-trello-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="49c4a-213">a.</span><span class="sxs-lookup"><span data-stu-id="49c4a-213">a.</span></span> <span data-ttu-id="49c4a-214">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="49c4a-214">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="49c4a-215">b.</span><span class="sxs-lookup"><span data-stu-id="49c4a-215">b.</span></span> <span data-ttu-id="49c4a-216">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="49c4a-216">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="49c4a-217">c.</span><span class="sxs-lookup"><span data-stu-id="49c4a-217">c.</span></span> <span data-ttu-id="49c4a-218">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="49c4a-218">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="49c4a-219">d.</span><span class="sxs-lookup"><span data-stu-id="49c4a-219">d.</span></span> <span data-ttu-id="49c4a-220">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="49c4a-220">Click **Create**.</span></span>
 
### <a name="creating-a-trello-test-user"></a><span data-ttu-id="49c4a-221">Tworzenie użytkownika testowego Trello</span><span class="sxs-lookup"><span data-stu-id="49c4a-221">Creating a Trello test user</span></span>

<span data-ttu-id="49c4a-222">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Trello.</span><span class="sxs-lookup"><span data-stu-id="49c4a-222">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="49c4a-223">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Trello.</span><span class="sxs-lookup"><span data-stu-id="49c4a-223">In this section, you create a user called Britta Simon in Trello.</span></span> <span data-ttu-id="49c4a-224">Trello obsługę w czasie i nowe konto jest tworzone powitania po raz pierwszy logowania z usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="49c4a-224">Trello supports just-in-time provisioning and a new account is created hello first time you sign in from Azure AD.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="49c4a-225">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="49c4a-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="49c4a-226">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooTrello.</span><span class="sxs-lookup"><span data-stu-id="49c4a-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooTrello.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="49c4a-228">**tooassign tooTrello Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="49c4a-228">**tooassign Britta Simon tooTrello, perform hello following steps:**</span></span>

1. <span data-ttu-id="49c4a-229">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="49c4a-229">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="49c4a-231">Z listy aplikacji hello wybierz **Trello**.</span><span class="sxs-lookup"><span data-stu-id="49c4a-231">In hello applications list, select **Trello**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-trello-tutorial/tutorial_trello_app.png) 

3. <span data-ttu-id="49c4a-233">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="49c4a-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="49c4a-235">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="49c4a-235">Click **Add** button.</span></span> <span data-ttu-id="49c4a-236">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="49c4a-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="49c4a-238">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="49c4a-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="49c4a-239">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="49c4a-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="49c4a-240">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="49c4a-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="49c4a-241">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="49c4a-241">Testing single sign-on</span></span>

<span data-ttu-id="49c4a-242">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="49c4a-242">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="49c4a-243">Po kliknięciu kafelka Trello hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Trello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="49c4a-243">When you click hello Trello tile in hello Access Panel, you should get automatically signed-on tooyour Trello application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="49c4a-244">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="49c4a-244">Additional resources</span></span>

* [<span data-ttu-id="49c4a-245">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="49c4a-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="49c4a-246">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="49c4a-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-trello-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-trello-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-trello-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-trello-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-trello-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-trello-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-trello-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-trello-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-trello-tutorial/tutorial_general_203.png

