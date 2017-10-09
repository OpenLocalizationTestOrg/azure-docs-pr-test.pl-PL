---
title: "Samouczek: Integracji Azure Active Directory z innowacji współpracy | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i innowacji współpracy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bba95df3-75a4-4a93-8805-b3a8aa3d4861
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: e85fabfe11a380129f319a101aa7c7a9491260f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-collaborative-innovation"></a><span data-ttu-id="85a6f-103">Samouczek: Integracji Azure Active Directory z innowacji współpracy</span><span class="sxs-lookup"><span data-stu-id="85a6f-103">Tutorial: Azure Active Directory integration with Collaborative Innovation</span></span>

<span data-ttu-id="85a6f-104">Z tego samouczka, dowiesz się, jak toointegrate innowacji współpracy z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="85a6f-104">In this tutorial, you learn how toointegrate Collaborative Innovation with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="85a6f-105">Integrowanie innowacji współpracy z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="85a6f-105">Integrating Collaborative Innovation with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="85a6f-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooCollaborative innowacji</span><span class="sxs-lookup"><span data-stu-id="85a6f-106">You can control in Azure AD who has access tooCollaborative Innovation</span></span>
- <span data-ttu-id="85a6f-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooCollaborative innowacji (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="85a6f-107">You can enable your users tooautomatically get signed-on tooCollaborative Innovation (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="85a6f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="85a6f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="85a6f-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="85a6f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85a6f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="85a6f-110">Prerequisites</span></span>

<span data-ttu-id="85a6f-111">tooconfigure integracji usługi Azure AD z innowacji współpracy należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="85a6f-111">tooconfigure Azure AD integration with Collaborative Innovation, you need hello following items:</span></span>

- <span data-ttu-id="85a6f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="85a6f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="85a6f-113">Wspólne innowacji jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="85a6f-113">A Collaborative Innovation single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="85a6f-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="85a6f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="85a6f-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="85a6f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="85a6f-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="85a6f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="85a6f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="85a6f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="85a6f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="85a6f-118">Scenario description</span></span>
<span data-ttu-id="85a6f-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="85a6f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="85a6f-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="85a6f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="85a6f-121">Dodawanie innowacji współpracy z galerii hello</span><span class="sxs-lookup"><span data-stu-id="85a6f-121">Adding Collaborative Innovation from hello gallery</span></span>
2. <span data-ttu-id="85a6f-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="85a6f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-collaborative-innovation-from-hello-gallery"></a><span data-ttu-id="85a6f-123">Dodawanie innowacji współpracy z galerii hello</span><span class="sxs-lookup"><span data-stu-id="85a6f-123">Adding Collaborative Innovation from hello gallery</span></span>
<span data-ttu-id="85a6f-124">tooconfigure hello integracji innowacji współpracy z usługą Azure AD, należy tooadd innowacji współpracy z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="85a6f-124">tooconfigure hello integration of Collaborative Innovation into Azure AD, you need tooadd Collaborative Innovation from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="85a6f-125">**tooadd innowacji współpracy z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="85a6f-125">**tooadd Collaborative Innovation from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="85a6f-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="85a6f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="85a6f-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="85a6f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="85a6f-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="85a6f-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="85a6f-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="85a6f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="85a6f-133">W polu wyszukiwania hello wpisz **innowacji współpracy**.</span><span class="sxs-lookup"><span data-stu-id="85a6f-133">In hello search box, type **Collaborative Innovation**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_search.png)

5. <span data-ttu-id="85a6f-135">W panelu wyników hello, wybierz **innowacji współpracy**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="85a6f-135">In hello results panel, select **Collaborative Innovation**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="85a6f-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="85a6f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="85a6f-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z współpracy innowacje oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="85a6f-138">In this section, you configure and test Azure AD single sign-on with Collaborative Innovation based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="85a6f-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w współpracy innowacji jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="85a6f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Collaborative Innovation is tooa user in Azure AD.</span></span> <span data-ttu-id="85a6f-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w współpracy innowacji musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="85a6f-140">In other words, a link relationship between an Azure AD user and hello related user in Collaborative Innovation needs toobe established.</span></span>

<span data-ttu-id="85a6f-141">W współpracy innowacji, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="85a6f-141">In Collaborative Innovation, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="85a6f-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z współpracy innowacji, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="85a6f-142">tooconfigure and test Azure AD single sign-on with Collaborative Innovation, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="85a6f-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="85a6f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="85a6f-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="85a6f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="85a6f-145">**[Tworzenie użytkownika testowego współpracy innowacji](#creating-a-collaborative-innovation-test-user)**  -toohave odpowiednikiem Simona Britta w współpracy innowacji, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="85a6f-145">**[Creating a Collaborative Innovation test user](#creating-a-collaborative-innovation-test-user)** - toohave a counterpart of Britta Simon in Collaborative Innovation that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="85a6f-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="85a6f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="85a6f-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="85a6f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="85a6f-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="85a6f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="85a6f-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji innowacji współpracy.</span><span class="sxs-lookup"><span data-stu-id="85a6f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Collaborative Innovation application.</span></span>

<span data-ttu-id="85a6f-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z współpracy innowacji, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="85a6f-150">**tooconfigure Azure AD single sign-on with Collaborative Innovation, perform hello following steps:**</span></span>

1. <span data-ttu-id="85a6f-151">W portalu Azure na powitania hello **innowacji współpracy** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="85a6f-151">In hello Azure portal, on hello **Collaborative Innovation** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="85a6f-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="85a6f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_samlbase.png)

3. <span data-ttu-id="85a6f-155">Na powitania **adresy URL i współpracy domeny innowacji** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="85a6f-155">On hello **Collaborative Innovation Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_url.png)

    <span data-ttu-id="85a6f-157">a.</span><span class="sxs-lookup"><span data-stu-id="85a6f-157">a.</span></span> <span data-ttu-id="85a6f-158">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<instancename>.foundry.<companyname>.com/`</span><span class="sxs-lookup"><span data-stu-id="85a6f-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<instancename>.foundry.<companyname>.com/`</span></span>

    <span data-ttu-id="85a6f-159">b.</span><span class="sxs-lookup"><span data-stu-id="85a6f-159">b.</span></span> <span data-ttu-id="85a6f-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<instancename>.foundry.<companyname>.com`</span><span class="sxs-lookup"><span data-stu-id="85a6f-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.foundry.<companyname>.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="85a6f-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="85a6f-161">These values are not real.</span></span> <span data-ttu-id="85a6f-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="85a6f-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="85a6f-163">Skontaktuj się z [zespołem pomocy technicznej współpracy klienta innowacji](https://www.unilever.com/contact/) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="85a6f-163">Contact [Collaborative Innovation Client support team](https://www.unilever.com/contact/) tooget these values.</span></span>  

4. <span data-ttu-id="85a6f-164">Wspólne aplikacji innowacji oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="85a6f-164">Collaborative Innovation application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="85a6f-165">Skonfiguruj powitania po oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="85a6f-165">Please configure hello following claims for this application.</span></span> <span data-ttu-id="85a6f-166">Można zarządzać hello wartości tych atrybutów z hello "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="85a6f-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="85a6f-167">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="85a6f-167">hello following screenshot shows an example for this.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-collaborativeinnovation-tutorial/attribute.png)
    
5. <span data-ttu-id="85a6f-169">Kliknij przycisk **widoku i edytować wszystkie atrybuty użytkowników** checkbox w hello **atrybuty użytkownika** sekcji tooexpand hello atrybutów.</span><span class="sxs-lookup"><span data-stu-id="85a6f-169">Click **View and edit all other user attributes** checkbox in hello **User Attributes** section tooexpand hello attributes.</span></span> <span data-ttu-id="85a6f-170">Wykonaj następujące kroki na każdym z atrybutów hello wyświetlane - hello</span><span class="sxs-lookup"><span data-stu-id="85a6f-170">Perform hello following steps on each of hello displayed attributes-</span></span>

    | <span data-ttu-id="85a6f-171">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="85a6f-171">Attribute Name</span></span> | <span data-ttu-id="85a6f-172">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="85a6f-172">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="85a6f-173">Imię</span><span class="sxs-lookup"><span data-stu-id="85a6f-173">givenname</span></span> | <span data-ttu-id="85a6f-174">User.givenName</span><span class="sxs-lookup"><span data-stu-id="85a6f-174">user.givenname</span></span> |
    | <span data-ttu-id="85a6f-175">nazwisko</span><span class="sxs-lookup"><span data-stu-id="85a6f-175">surname</span></span> | <span data-ttu-id="85a6f-176">User.surname</span><span class="sxs-lookup"><span data-stu-id="85a6f-176">user.surname</span></span> |
    | <span data-ttu-id="85a6f-177">emailaddress</span><span class="sxs-lookup"><span data-stu-id="85a6f-177">emailaddress</span></span> | <span data-ttu-id="85a6f-178">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="85a6f-178">user.userprincipalname</span></span> |
    | <span data-ttu-id="85a6f-179">name</span><span class="sxs-lookup"><span data-stu-id="85a6f-179">name</span></span> | <span data-ttu-id="85a6f-180">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="85a6f-180">user.userprincipalname</span></span> |

    <span data-ttu-id="85a6f-181">a.</span><span class="sxs-lookup"><span data-stu-id="85a6f-181">a.</span></span> <span data-ttu-id="85a6f-182">Kliknij przycisk hello atrybutu tooopen hello **atrybutu Edytuj** okna.</span><span class="sxs-lookup"><span data-stu-id="85a6f-182">Click hello attribute tooopen hello **Edit Attribute** window.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-collaborativeinnovation-tutorial/url_update.png)

    <span data-ttu-id="85a6f-184">b.</span><span class="sxs-lookup"><span data-stu-id="85a6f-184">b.</span></span> <span data-ttu-id="85a6f-185">Usuń wartość adresu URL hello z hello **Namespace**.</span><span class="sxs-lookup"><span data-stu-id="85a6f-185">Delete hello URL value from hello **Namespace**.</span></span>
    
    <span data-ttu-id="85a6f-186">c.</span><span class="sxs-lookup"><span data-stu-id="85a6f-186">c.</span></span> <span data-ttu-id="85a6f-187">Kliknij przycisk **Ok** toosave hello ustawienie.</span><span class="sxs-lookup"><span data-stu-id="85a6f-187">Click **Ok** toosave hello setting.</span></span>

6. <span data-ttu-id="85a6f-188">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="85a6f-188">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_certificate.png) 

7. <span data-ttu-id="85a6f-190">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="85a6f-190">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="85a6f-192">tooconfigure rejestracji jednokrotnej w **innowacji współpracy** strony, należy pobrać hello toosend **XML metadanych** za[innowacji współpracy z pomocą techniczną](https://www.unilever.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="85a6f-192">tooconfigure single sign-on on **Collaborative Innovation** side, you need toosend hello downloaded **Metadata XML** too[Collaborative Innovation support team](https://www.unilever.com/contact/).</span></span> <span data-ttu-id="85a6f-193">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="85a6f-193">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="85a6f-194">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="85a6f-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="85a6f-195">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="85a6f-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="85a6f-196">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="85a6f-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="85a6f-197">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="85a6f-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="85a6f-198">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="85a6f-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="85a6f-200">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="85a6f-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="85a6f-201">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="85a6f-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="85a6f-203">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="85a6f-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="85a6f-205">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="85a6f-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="85a6f-207">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="85a6f-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-collaborativeinnovation-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="85a6f-209">a.</span><span class="sxs-lookup"><span data-stu-id="85a6f-209">a.</span></span> <span data-ttu-id="85a6f-210">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="85a6f-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="85a6f-211">b.</span><span class="sxs-lookup"><span data-stu-id="85a6f-211">b.</span></span> <span data-ttu-id="85a6f-212">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="85a6f-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="85a6f-213">c.</span><span class="sxs-lookup"><span data-stu-id="85a6f-213">c.</span></span> <span data-ttu-id="85a6f-214">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="85a6f-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="85a6f-215">d.</span><span class="sxs-lookup"><span data-stu-id="85a6f-215">d.</span></span> <span data-ttu-id="85a6f-216">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="85a6f-216">Click **Create**.</span></span>
 
### <a name="creating-a-collaborative-innovation-test-user"></a><span data-ttu-id="85a6f-217">Tworzenie użytkownika testowego innowacji współpracy</span><span class="sxs-lookup"><span data-stu-id="85a6f-217">Creating a Collaborative Innovation test user</span></span>

<span data-ttu-id="85a6f-218">toolog użytkowników tooenable usługi Azure AD w tooCollaborative innowacji, muszą mieć przydzielone do współpracy innowacji.</span><span class="sxs-lookup"><span data-stu-id="85a6f-218">tooenable Azure AD users toolog in tooCollaborative Innovation, they must be provisioned into Collaborative Innovation.</span></span>  

<span data-ttu-id="85a6f-219">W przypadku tej aplikacji udostępniania odbywa się automatycznie jako aplikacji hello obsługuje tylko w czasie Inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="85a6f-219">In case of this application provisioning is automatic as hello application supports just in time user provisioning.</span></span> <span data-ttu-id="85a6f-220">Dlatego nie ma tooperform nie potrzeba żadnych czynności w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="85a6f-220">So there is no need tooperform any steps here.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="85a6f-221">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="85a6f-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="85a6f-222">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooCollaborative innowacji.</span><span class="sxs-lookup"><span data-stu-id="85a6f-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCollaborative Innovation.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="85a6f-224">**tooassign tooCollaborative Simona Britta innowacji, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="85a6f-224">**tooassign Britta Simon tooCollaborative Innovation, perform hello following steps:**</span></span>

1. <span data-ttu-id="85a6f-225">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="85a6f-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="85a6f-227">Z listy aplikacji hello wybierz **innowacji współpracy**.</span><span class="sxs-lookup"><span data-stu-id="85a6f-227">In hello applications list, select **Collaborative Innovation**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_collaborativeinnovation_app.png) 

3. <span data-ttu-id="85a6f-229">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="85a6f-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="85a6f-231">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="85a6f-231">Click **Add** button.</span></span> <span data-ttu-id="85a6f-232">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="85a6f-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="85a6f-234">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="85a6f-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="85a6f-235">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="85a6f-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="85a6f-236">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="85a6f-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="85a6f-237">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="85a6f-237">Testing single sign-on</span></span>

<span data-ttu-id="85a6f-238">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="85a6f-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="85a6f-239">Po kliknięciu kafelka współpracy innowacji hello w hello Panel dostępu, należy pobrać strony logowania aplikacji innowacji współpracy.</span><span class="sxs-lookup"><span data-stu-id="85a6f-239">When you click hello Collaborative Innovation tile in hello Access Panel, you should get login page of Collaborative Innovation application.</span></span>
<span data-ttu-id="85a6f-240">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="85a6f-240">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="85a6f-241">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="85a6f-241">Additional resources</span></span>

* [<span data-ttu-id="85a6f-242">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="85a6f-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="85a6f-243">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="85a6f-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-collaborativeinnovation-tutorial/tutorial_general_203.png

