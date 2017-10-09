---
title: 'Samouczek: Integracji Azure Active Directory z centralnego Cerner | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Cerner centralnego."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2bc549d-d286-4679-854e-bb67c62b0475
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 3493d180e8f229b7cd228769f780f10208114889
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cerner-central"></a><span data-ttu-id="8ac11-103">Samouczek: Integracji Azure Active Directory z centralnego Cerner</span><span class="sxs-lookup"><span data-stu-id="8ac11-103">Tutorial: Azure Active Directory integration with Cerner Central</span></span>

<span data-ttu-id="8ac11-104">Z tego samouczka, dowiesz się, jak toointegrate Cerner centralnego w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8ac11-104">In this tutorial, you learn how toointegrate Cerner Central with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8ac11-105">Integracja z usługą Azure AD Cerner centralnego zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="8ac11-105">Integrating Cerner Central with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="8ac11-106">Można kontrolować w usłudze Azure AD, kto ma dostęp tooCerner środkowe</span><span class="sxs-lookup"><span data-stu-id="8ac11-106">You can control in Azure AD who has access tooCerner Central</span></span>
- <span data-ttu-id="8ac11-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooCerner Środkowa (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ac11-107">You can enable your users tooautomatically get signed-on tooCerner Central (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8ac11-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="8ac11-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="8ac11-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8ac11-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ac11-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="8ac11-110">Prerequisites</span></span>

<span data-ttu-id="8ac11-111">tooconfigure integracji usługi Azure AD z centralnego Cerner należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8ac11-111">tooconfigure Azure AD integration with Cerner Central, you need hello following items:</span></span>

- <span data-ttu-id="8ac11-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ac11-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8ac11-113">Zatwierdzone Cerner centralna konta systemu</span><span class="sxs-lookup"><span data-stu-id="8ac11-113">An approved Cerner Central System Account</span></span>

> [!NOTE]
> <span data-ttu-id="8ac11-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="8ac11-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8ac11-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="8ac11-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8ac11-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="8ac11-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8ac11-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ac11-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8ac11-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="8ac11-118">Scenario description</span></span>
<span data-ttu-id="8ac11-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="8ac11-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8ac11-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="8ac11-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8ac11-121">Dodawanie centralnego Cerner z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8ac11-121">Adding Cerner Central from hello gallery</span></span>
2. <span data-ttu-id="8ac11-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8ac11-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cerner-central-from-hello-gallery"></a><span data-ttu-id="8ac11-123">Dodawanie centralnego Cerner z galerii hello</span><span class="sxs-lookup"><span data-stu-id="8ac11-123">Adding Cerner Central from hello gallery</span></span>
<span data-ttu-id="8ac11-124">tooconfigure hello integracji Cerner centralnego w usłudze Azure Active Directory, należy tooadd centralnego Cerner z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="8ac11-124">tooconfigure hello integration of Cerner Central into Azure AD, you need tooadd Cerner Central from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="8ac11-125">**tooadd centralnego Cerner z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="8ac11-125">**tooadd Cerner Central from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ac11-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8ac11-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="8ac11-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="8ac11-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="8ac11-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8ac11-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="8ac11-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry okna dialogowego hello.</span><span class="sxs-lookup"><span data-stu-id="8ac11-131">tooadd new application, click **New application** button on top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="8ac11-133">W polu wyszukiwania hello wpisz **centralnego Cerner**.</span><span class="sxs-lookup"><span data-stu-id="8ac11-133">In hello search box, type **Cerner Central**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_search.png)

5. <span data-ttu-id="8ac11-135">W panelu wyników hello, wybierz **centralnego Cerner**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8ac11-135">In hello results panel, select **Cerner Central**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8ac11-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="8ac11-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8ac11-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z centralnego Cerner oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="8ac11-138">In this section, you configure and test Azure AD single sign-on with Cerner Central based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8ac11-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w środkowej Cerner jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ac11-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Cerner Central is tooa user in Azure AD.</span></span> <span data-ttu-id="8ac11-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w środkowej Cerner musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="8ac11-140">In other words, a link relationship between an Azure AD user and hello related user in Cerner Central needs toobe established.</span></span>

<span data-ttu-id="8ac11-141">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z centralnego Cerner, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="8ac11-141">tooconfigure and test Azure AD single sign-on with Cerner Central, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="8ac11-142">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="8ac11-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="8ac11-143">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8ac11-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8ac11-144">**[Tworzenie użytkownika testowego centralnego Cerner](#creating-a-cerner-central-test-user)**  -toohave odpowiednikiem Simona Britta środkowej Cerner, będący toohello połączonej usługi Azure AD reprezentację hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8ac11-144">**[Creating a Cerner Central test user](#creating-a-cerner-central-test-user)** - toohave a counterpart of Britta Simon in Cerner Central that is linked toohello Azure AD representation of hello user.</span></span>
4. <span data-ttu-id="8ac11-145">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8ac11-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8ac11-146">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="8ac11-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8ac11-147">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8ac11-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8ac11-148">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji Cerner centralnego.</span><span class="sxs-lookup"><span data-stu-id="8ac11-148">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Cerner Central application.</span></span>

<span data-ttu-id="8ac11-149">**tooconfigure usługi Azure AD rejestracji jednokrotnej z centralnego Cerner wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="8ac11-149">**tooconfigure Azure AD single sign-on with Cerner Central, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ac11-150">W portalu Azure na powitania hello **centralnego Cerner** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="8ac11-150">In hello Azure portal, on hello **Cerner Central** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="8ac11-152">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="8ac11-152">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_samlbase.png)

3. <span data-ttu-id="8ac11-154">Na powitania **Cerner centralnej domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8ac11-154">On hello **Cerner Central Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_url.png)

    <span data-ttu-id="8ac11-156">a.</span><span class="sxs-lookup"><span data-stu-id="8ac11-156">a.</span></span> <span data-ttu-id="8ac11-157">W hello **identyfikator** pole tekstowe, wartość hello typu przy użyciu następującego wzorce hello:</span><span class="sxs-lookup"><span data-stu-id="8ac11-157">In hello **Identifier** textbox, type hello value using hello following patterns:</span></span>
    
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcerner.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://sandboxcernercentral.com/session-api/protocol/saml2/metadata` |
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/metadata` |

    <span data-ttu-id="8ac11-158">b.</span><span class="sxs-lookup"><span data-stu-id="8ac11-158">b.</span></span> <span data-ttu-id="8ac11-159">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL przy użyciu następującego hello wzorców:</span><span class="sxs-lookup"><span data-stu-id="8ac11-159">In hello **Reply URL** textbox, type a URL using hello following patterns:</span></span> 
    | |
    |--|
    | `https://<instancename>.cernercentral.com/session-api/protocol/saml2/sso` |
    | `https://cernercentral.com/<instasncename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://sandboxcernercentral.com/<instancename>` |
    | `https://<subdomain>.sandboxcernercentral.com/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="8ac11-160">Wartości te nie są hello prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="8ac11-160">These values are not hello real.</span></span> <span data-ttu-id="8ac11-161">Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="8ac11-161">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="8ac11-162">Skontaktuj się z [zespołem pomocy technicznej centralnego Cerner](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="8ac11-162">Contact [Cerner Central support team](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations) tooget these values.</span></span>
 
4. <span data-ttu-id="8ac11-163">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8ac11-163">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cernercentral-tutorial/tutorial_general_400.png)

5. <span data-ttu-id="8ac11-165">Witaj toogenerate **metadanych** adres url, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8ac11-165">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="8ac11-166">a.</span><span class="sxs-lookup"><span data-stu-id="8ac11-166">a.</span></span> <span data-ttu-id="8ac11-167">Kliknij przycisk **rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="8ac11-167">Click **App registrations**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appregistrations.png)
   
    <span data-ttu-id="8ac11-169">b.</span><span class="sxs-lookup"><span data-stu-id="8ac11-169">b.</span></span> <span data-ttu-id="8ac11-170">Kliknij przycisk **punkty końcowe** tooopen **punkty końcowe** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="8ac11-170">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpointicon.png)

    <span data-ttu-id="8ac11-172">c.</span><span class="sxs-lookup"><span data-stu-id="8ac11-172">c.</span></span> <span data-ttu-id="8ac11-173">Kliknij przycisk toocopy przycisku Kopiuj hello **dokument METADANYCH usług FEDERACYJNYCH** adresu url i wklej go do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="8ac11-173">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_endpoint.png)
     
    <span data-ttu-id="8ac11-175">d.</span><span class="sxs-lookup"><span data-stu-id="8ac11-175">d.</span></span> <span data-ttu-id="8ac11-176">Teraz przejdź strony właściwości toohello **centralnego Cerner** i hello kopii **identyfikator aplikacji** przy użyciu **kopii** przycisk i wklej go do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="8ac11-176">Now go toohello property page of **Cerner Central** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_appid.png)

    <span data-ttu-id="8ac11-178">e.</span><span class="sxs-lookup"><span data-stu-id="8ac11-178">e.</span></span> <span data-ttu-id="8ac11-179">Generowanie hello **adres URL metadanych** przy użyciu hello następującego wzorca:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="8ac11-179">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

6. <span data-ttu-id="8ac11-180">tooconfigure rejestracji jednokrotnej w **centralnego Cerner** obok siebie, potrzebujesz toosend hello **adres URL metadanych** zbyt[centralnego Cerner Obsługa](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span><span class="sxs-lookup"><span data-stu-id="8ac11-180">tooconfigure single sign-on on **Cerner Central** side, you need toosend hello **Metadata URL** too[Cerner Central support](https://wiki.ucern.com/display/CernerCentral/Contacting+Cloud+Operations).</span></span> <span data-ttu-id="8ac11-181">Skonfigurowano hello logowania jednokrotnego dla aplikacji po stronie toocomplete hello integracji.</span><span class="sxs-lookup"><span data-stu-id="8ac11-181">They configure hello SSO on application side toocomplete hello integration.</span></span>

> [!TIP]
> <span data-ttu-id="8ac11-182">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="8ac11-182">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="8ac11-183">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="8ac11-183">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="8ac11-184">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="8ac11-184">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8ac11-185">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ac11-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="8ac11-186">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="8ac11-186">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span> 

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="8ac11-188">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8ac11-188">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ac11-189">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="8ac11-189">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8ac11-191">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="8ac11-191">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8ac11-193">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="8ac11-193">tooopen hello **User** dialog, click **Add**.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8ac11-195">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8ac11-195">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-cernercentral-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8ac11-197">a.</span><span class="sxs-lookup"><span data-stu-id="8ac11-197">a.</span></span> <span data-ttu-id="8ac11-198">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8ac11-198">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8ac11-199">b.</span><span class="sxs-lookup"><span data-stu-id="8ac11-199">b.</span></span> <span data-ttu-id="8ac11-200">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="8ac11-200">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="8ac11-201">c.</span><span class="sxs-lookup"><span data-stu-id="8ac11-201">c.</span></span> <span data-ttu-id="8ac11-202">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="8ac11-202">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="8ac11-203">d.</span><span class="sxs-lookup"><span data-stu-id="8ac11-203">d.</span></span> <span data-ttu-id="8ac11-204">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="8ac11-204">Click **Create**.</span></span>
 
### <a name="creating-a-cerner-central-test-user"></a><span data-ttu-id="8ac11-205">Tworzenie użytkownika testowego Cerner środkowe</span><span class="sxs-lookup"><span data-stu-id="8ac11-205">Creating a Cerner Central test user</span></span>

<span data-ttu-id="8ac11-206">**Środkowe Cerner** aplikacji pozwala na uwierzytelnianie z każdego dostawcy tożsamości federacyjnych.</span><span class="sxs-lookup"><span data-stu-id="8ac11-206">**Cerner Central** application allows authentication from any federated identity provider.</span></span> <span data-ttu-id="8ac11-207">Jeśli użytkownik jest w stanie toolog na stronie głównej aplikacji toohello, są federacyjnych i nie potrzebują ręcznej obsługi.</span><span class="sxs-lookup"><span data-stu-id="8ac11-207">If a user is able toolog in toohello application home page, they are federated and have no need for any manual provisioning.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="8ac11-208">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ac11-208">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="8ac11-209">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooCerner centralnego.</span><span class="sxs-lookup"><span data-stu-id="8ac11-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooCerner Central.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="8ac11-211">**tooassign tooCerner Simona Britta centralnego, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="8ac11-211">**tooassign Britta Simon tooCerner Central, perform hello following steps:**</span></span>

1. <span data-ttu-id="8ac11-212">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="8ac11-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="8ac11-214">Z listy aplikacji hello wybierz **centralnego Cerner**.</span><span class="sxs-lookup"><span data-stu-id="8ac11-214">In hello applications list, select **Cerner Central**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-cernercentral-tutorial/tutorial_cernercentral_app.png) 

3. <span data-ttu-id="8ac11-216">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="8ac11-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="8ac11-218">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="8ac11-218">Click **Add** button.</span></span> <span data-ttu-id="8ac11-219">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ac11-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="8ac11-221">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="8ac11-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="8ac11-222">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ac11-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8ac11-223">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8ac11-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8ac11-224">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8ac11-224">Testing single sign-on</span></span>

<span data-ttu-id="8ac11-225">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8ac11-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="8ac11-226">Po kliknięciu hello centralnego Cerner kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour centralnego Cerner aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8ac11-226">When you click hello Cerner Central tile in hello Access Panel, you should get automatically signed-on tooyour Cerner Central application.</span></span> <span data-ttu-id="8ac11-227">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8ac11-227">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8ac11-228">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="8ac11-228">Additional resources</span></span>

* [<span data-ttu-id="8ac11-229">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ac11-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8ac11-230">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8ac11-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cernercentral-tutorial/tutorial_general_203.png

