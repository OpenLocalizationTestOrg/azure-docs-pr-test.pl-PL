---
title: 'Samouczek: Integracji Azure Active Directory z FreshGrade | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i FreshGrade."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1055bba6-f4df-462e-bc9b-1ad5ada0f638
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: e2fe7cedd45290945ec5624453a9675abdd7726d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshgrade"></a><span data-ttu-id="4424f-103">Samouczek: Integracji Azure Active Directory z FreshGrade</span><span class="sxs-lookup"><span data-stu-id="4424f-103">Tutorial: Azure Active Directory integration with FreshGrade</span></span>

<span data-ttu-id="4424f-104">Z tego samouczka, dowiesz się, jak toointegrate FreshGrade w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4424f-104">In this tutorial, you learn how toointegrate FreshGrade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4424f-105">Integracja z usługą Azure AD FreshGrade zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="4424f-105">Integrating FreshGrade with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4424f-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooFreshGrade</span><span class="sxs-lookup"><span data-stu-id="4424f-106">You can control in Azure AD who has access tooFreshGrade</span></span>
- <span data-ttu-id="4424f-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooFreshGrade (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4424f-107">You can enable your users tooautomatically get signed-on tooFreshGrade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4424f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="4424f-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4424f-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4424f-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4424f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4424f-110">Prerequisites</span></span>

<span data-ttu-id="4424f-111">tooconfigure integracji z usługą Azure AD z FreshGrade należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="4424f-111">tooconfigure Azure AD integration with FreshGrade, you need hello following items:</span></span>

- <span data-ttu-id="4424f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4424f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4424f-113">FreshGrade logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="4424f-113">A FreshGrade single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4424f-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="4424f-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4424f-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="4424f-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4424f-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="4424f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4424f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4424f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4424f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="4424f-118">Scenario description</span></span>
<span data-ttu-id="4424f-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="4424f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4424f-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="4424f-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4424f-121">Dodawanie FreshGrade z galerii hello</span><span class="sxs-lookup"><span data-stu-id="4424f-121">Adding FreshGrade from hello gallery</span></span>
2. <span data-ttu-id="4424f-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4424f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshgrade-from-hello-gallery"></a><span data-ttu-id="4424f-123">Dodawanie FreshGrade z galerii hello</span><span class="sxs-lookup"><span data-stu-id="4424f-123">Adding FreshGrade from hello gallery</span></span>
<span data-ttu-id="4424f-124">tooconfigure hello integracji FreshGrade do usługi Azure AD, należy tooadd FreshGrade z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="4424f-124">tooconfigure hello integration of FreshGrade into Azure AD, you need tooadd FreshGrade from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4424f-125">**tooadd FreshGrade z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4424f-125">**tooadd FreshGrade from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4424f-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4424f-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="4424f-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="4424f-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4424f-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4424f-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="4424f-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4424f-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="4424f-133">W polu wyszukiwania hello wpisz **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="4424f-133">In hello search box, type **FreshGrade**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_search.png)

5. <span data-ttu-id="4424f-135">W panelu wyników hello zaznacz **FreshGrade**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="4424f-135">In hello results panel, select **FreshGrade**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4424f-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="4424f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4424f-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z FreshGrade w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="4424f-138">In this section, you configure and test Azure AD single sign-on with FreshGrade based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4424f-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w FreshGrade jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4424f-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FreshGrade is tooa user in Azure AD.</span></span> <span data-ttu-id="4424f-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w FreshGrade musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="4424f-140">In other words, a link relationship between an Azure AD user and hello related user in FreshGrade needs toobe established.</span></span>

<span data-ttu-id="4424f-141">W FreshGrade, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="4424f-141">In FreshGrade, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4424f-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z FreshGrade, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="4424f-142">tooconfigure and test Azure AD single sign-on with FreshGrade, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4424f-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="4424f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4424f-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="4424f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4424f-145">**[Tworzenie użytkownika testowego FreshGrade](#creating-a-freshgrade-test-user)**  -toohave odpowiednikiem Simona Britta w FreshGrade, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="4424f-145">**[Creating a FreshGrade test user](#creating-a-freshgrade-test-user)** - toohave a counterpart of Britta Simon in FreshGrade that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4424f-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="4424f-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4424f-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="4424f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4424f-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4424f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4424f-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="4424f-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your FreshGrade application.</span></span>

<span data-ttu-id="4424f-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z FreshGrade, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4424f-150">**tooconfigure Azure AD single sign-on with FreshGrade, perform hello following steps:**</span></span>

1. <span data-ttu-id="4424f-151">W portalu Azure na powitania hello **FreshGrade** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="4424f-151">In hello Azure portal, on hello **FreshGrade** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="4424f-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="4424f-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_samlbase.png)

3. <span data-ttu-id="4424f-155">Na powitania **FreshGrade domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="4424f-155">On hello **FreshGrade Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_url.png)

    <span data-ttu-id="4424f-157">a.</span><span class="sxs-lookup"><span data-stu-id="4424f-157">a.</span></span> <span data-ttu-id="4424f-158">W hello **adres URL logowania** tekstowym, wpisz adres URL przy użyciu następującego hello wzorców:</span><span class="sxs-lookup"><span data-stu-id="4424f-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
      | |
      |--|
      | `https://<subdomain>.freshgrade.com/login` |    
      | `https://<subdomain>.onboarding.freshgrade.com/login` |

    <span data-ttu-id="4424f-159">b.</span><span class="sxs-lookup"><span data-stu-id="4424f-159">b.</span></span> <span data-ttu-id="4424f-160">W hello **identyfikator** tekstowym, wpisz adres URL przy użyciu następującego hello wzorców:</span><span class="sxs-lookup"><span data-stu-id="4424f-160">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
      | |
      |--|
      | `https://login.onboarding.freshgrade.com:443/saml/metadata/alias/<instancename>` |      
      | `https://login.freshgrade.com:443/saml/metadata/alias/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="4424f-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="4424f-161">These values are not real.</span></span> <span data-ttu-id="4424f-162">Zaktualizować te wartości z hello rzeczywisty adres URL logowania i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="4424f-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4424f-163">Skontaktuj się z [zespołem pomocy technicznej klienta FreshGrade](mailTo:support@freshgrade.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="4424f-163">Contact [FreshGrade Client support team](mailTo:support@freshgrade.com) tooget these values.</span></span> 
 


4. <span data-ttu-id="4424f-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="4424f-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_certificate.png) 

5. <span data-ttu-id="4424f-166">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4424f-166">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshgrade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4424f-168">Na powitania **konfiguracji FreshGrade** kliknij **skonfigurować FreshGrade** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="4424f-168">On hello **FreshGrade Configuration** section, click **Configure FreshGrade** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4424f-169">Kopiuj hello **SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="4424f-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_configure.png) 

7. <span data-ttu-id="4424f-171">Witaj toogenerate **metadanych** adres url, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="4424f-171">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="4424f-172">a.</span><span class="sxs-lookup"><span data-stu-id="4424f-172">a.</span></span> <span data-ttu-id="4424f-173">Kliknij przycisk **rejestracji aplikacji**.</span><span class="sxs-lookup"><span data-stu-id="4424f-173">Click **App registrations**.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appregistrations.png)
   
    <span data-ttu-id="4424f-175">b.</span><span class="sxs-lookup"><span data-stu-id="4424f-175">b.</span></span> <span data-ttu-id="4424f-176">Kliknij przycisk **punkty końcowe** tooopen **punkty końcowe** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="4424f-176">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpointicon.png)

    <span data-ttu-id="4424f-178">c.</span><span class="sxs-lookup"><span data-stu-id="4424f-178">c.</span></span> <span data-ttu-id="4424f-179">Kliknij przycisk toocopy przycisku Kopiuj hello **dokument METADANYCH usług FEDERACYJNYCH** adresu url i wklej go do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="4424f-179">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpoint.png)
     
    <span data-ttu-id="4424f-181">d.</span><span class="sxs-lookup"><span data-stu-id="4424f-181">d.</span></span> <span data-ttu-id="4424f-182">Teraz przejdź strony właściwości toohello **FreshGrade** i kopiowania hello **identyfikator aplikacji** przy użyciu **kopiowania** przycisk i wklej go do Notatnika.</span><span class="sxs-lookup"><span data-stu-id="4424f-182">Now go toohello property page of **FreshGrade** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appid.png)

    <span data-ttu-id="4424f-184">e.</span><span class="sxs-lookup"><span data-stu-id="4424f-184">e.</span></span> <span data-ttu-id="4424f-185">Generowanie hello **adres URL metadanych** przy użyciu hello następującego wzorca:`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="4424f-185">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

8. <span data-ttu-id="4424f-186">tooconfigure rejestracji jednokrotnej w **FreshGrade** obok siebie, potrzebujesz toosend hello **adres URL metadanych** i **SAML pojedynczy znak na adres URL usługi** zbyt[FreshGrade obsługuje zespołu](mailTo:support@freshgrade.com).</span><span class="sxs-lookup"><span data-stu-id="4424f-186">tooconfigure single sign-on on **FreshGrade** side, you need toosend hello **Metadata URL** and **SAML Single Sign-On Service URL** too[FreshGrade support team](mailTo:support@freshgrade.com).</span></span> <span data-ttu-id="4424f-187">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="4424f-187">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="4424f-188">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="4424f-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4424f-189">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="4424f-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4424f-190">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4424f-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4424f-191">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="4424f-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="4424f-192">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="4424f-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="4424f-194">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="4424f-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4424f-195">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="4424f-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4424f-197">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="4424f-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4424f-199">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4424f-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4424f-201">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="4424f-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4424f-203">a.</span><span class="sxs-lookup"><span data-stu-id="4424f-203">a.</span></span> <span data-ttu-id="4424f-204">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4424f-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4424f-205">b.</span><span class="sxs-lookup"><span data-stu-id="4424f-205">b.</span></span> <span data-ttu-id="4424f-206">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4424f-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4424f-207">c.</span><span class="sxs-lookup"><span data-stu-id="4424f-207">c.</span></span> <span data-ttu-id="4424f-208">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="4424f-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4424f-209">d.</span><span class="sxs-lookup"><span data-stu-id="4424f-209">d.</span></span> <span data-ttu-id="4424f-210">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="4424f-210">Click **Create**.</span></span>
 
### <a name="creating-a-freshgrade-test-user"></a><span data-ttu-id="4424f-211">Tworzenie użytkownika testowego FreshGrade</span><span class="sxs-lookup"><span data-stu-id="4424f-211">Creating a FreshGrade test user</span></span>

<span data-ttu-id="4424f-212">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="4424f-212">In this section, you create a user called Britta Simon in FreshGrade.</span></span> <span data-ttu-id="4424f-213">We współpracy z [zespołem pomocy technicznej FreshGrade](mailTo:support@freshgrade.com) tooadd hello użytkowników hello FreshGrade platformy.</span><span class="sxs-lookup"><span data-stu-id="4424f-213">Please work with [FreshGrade support team](mailTo:support@freshgrade.com) tooadd hello users in hello FreshGrade platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4424f-214">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4424f-214">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4424f-215">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooFreshGrade.</span><span class="sxs-lookup"><span data-stu-id="4424f-215">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFreshGrade.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="4424f-217">**tooassign tooFreshGrade Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="4424f-217">**tooassign Britta Simon tooFreshGrade, perform hello following steps:**</span></span>

1. <span data-ttu-id="4424f-218">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="4424f-218">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="4424f-220">Z listy aplikacji hello wybierz **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="4424f-220">In hello applications list, select **FreshGrade**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_app.png) 

3. <span data-ttu-id="4424f-222">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="4424f-222">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="4424f-224">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="4424f-224">Click **Add** button.</span></span> <span data-ttu-id="4424f-225">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4424f-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="4424f-227">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="4424f-227">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4424f-228">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4424f-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4424f-229">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="4424f-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4424f-230">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="4424f-230">Testing single sign-on</span></span>

<span data-ttu-id="4424f-231">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="4424f-231">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="4424f-232">Po kliknięciu kafelka FreshGrade hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour FreshGrade aplikacji.</span><span class="sxs-lookup"><span data-stu-id="4424f-232">When you click hello FreshGrade tile in hello Access Panel, you should get automatically signed-on tooyour FreshGrade application.</span></span>
<span data-ttu-id="4424f-233">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4424f-233">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4424f-234">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="4424f-234">Additional resources</span></span>

* [<span data-ttu-id="4424f-235">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4424f-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4424f-236">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="4424f-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_203.png

