---
title: 'Samouczek: Integracji Azure Active Directory z obiektu ServiceChannel | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i obiektu ServiceChannel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 956371a1e99dcba4137c271ecfe8a62b9ec64a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a><span data-ttu-id="b3c93-103">Samouczek: Integracji Azure Active Directory z obiektu ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="b3c93-103">Tutorial: Azure Active Directory integration with ServiceChannel</span></span>

<span data-ttu-id="b3c93-104">Z tego samouczka, dowiesz się, jak toointegrate kanale usługi z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b3c93-104">In this tutorial, you learn how toointegrate ServiceChannel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b3c93-105">Integrowanie kanale usługi z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="b3c93-105">Integrating ServiceChannel with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b3c93-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooServiceChannel</span><span class="sxs-lookup"><span data-stu-id="b3c93-106">You can control in Azure AD who has access tooServiceChannel</span></span>
- <span data-ttu-id="b3c93-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooServiceChannel (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3c93-107">You can enable your users tooautomatically get signed-on tooServiceChannel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b3c93-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="b3c93-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="b3c93-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b3c93-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3c93-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b3c93-110">Prerequisites</span></span>

<span data-ttu-id="b3c93-111">tooconfigure integracji z usługą Azure AD z obiektu ServiceChannel należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="b3c93-111">tooconfigure Azure AD integration with ServiceChannel, you need hello following items:</span></span>

- <span data-ttu-id="b3c93-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3c93-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b3c93-113">Obiektu ServiceChannel jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="b3c93-113">A ServiceChannel single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b3c93-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="b3c93-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b3c93-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="b3c93-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b3c93-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="b3c93-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="b3c93-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b3c93-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b3c93-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="b3c93-118">Scenario description</span></span>
<span data-ttu-id="b3c93-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="b3c93-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b3c93-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="b3c93-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b3c93-121">Dodawanie obiektu ServiceChannel z galerii hello</span><span class="sxs-lookup"><span data-stu-id="b3c93-121">Adding ServiceChannel from hello gallery</span></span>
2. <span data-ttu-id="b3c93-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b3c93-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-servicechannel-from-hello-gallery"></a><span data-ttu-id="b3c93-123">Dodawanie obiektu ServiceChannel z galerii hello</span><span class="sxs-lookup"><span data-stu-id="b3c93-123">Adding ServiceChannel from hello gallery</span></span>
<span data-ttu-id="b3c93-124">tooconfigure hello integracji kanale usługi z usługą Azure AD, należy tooadd obiektu ServiceChannel z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="b3c93-124">tooconfigure hello integration of ServiceChannel into Azure AD, you need tooadd ServiceChannel from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b3c93-125">**tooadd obiektu ServiceChannel z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b3c93-125">**tooadd ServiceChannel from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3c93-126">W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b3c93-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="b3c93-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="b3c93-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b3c93-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b3c93-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="b3c93-131">Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3c93-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="b3c93-133">W polu wyszukiwania hello wpisz **obiektu ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="b3c93-133">In hello search box, type **ServiceChannel**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. <span data-ttu-id="b3c93-135">W panelu wyników hello zaznacz **obiektu ServiceChannel**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="b3c93-135">In hello results panel, select **ServiceChannel**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b3c93-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="b3c93-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b3c93-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z obiektu ServiceChannel w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="b3c93-138">In this section, you configure and test Azure AD single sign-on with ServiceChannel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b3c93-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w kanale usługi jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b3c93-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ServiceChannel is tooa user in Azure AD.</span></span> <span data-ttu-id="b3c93-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w kanale usługi musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="b3c93-140">In other words, a link relationship between an Azure AD user and hello related user in ServiceChannel needs toobe established.</span></span>

<span data-ttu-id="b3c93-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w kanale usługi.</span><span class="sxs-lookup"><span data-stu-id="b3c93-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ServiceChannel.</span></span>

<span data-ttu-id="b3c93-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z obiektu ServiceChannel, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="b3c93-142">tooconfigure and test Azure AD single sign-on with ServiceChannel, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b3c93-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="b3c93-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b3c93-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b3c93-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b3c93-145">**[Tworzenie użytkownika testowego obiektu ServiceChannel](#creating-a-servicechannel-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b3c93-145">**[Creating a ServiceChannel test user](#creating-a-servicechannel-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="b3c93-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="b3c93-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b3c93-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="b3c93-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b3c93-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b3c93-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b3c93-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji obiektu ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="b3c93-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your ServiceChannel application.</span></span>

<span data-ttu-id="b3c93-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z obiektu ServiceChannel, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b3c93-150">**tooconfigure Azure AD single sign-on with ServiceChannel, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3c93-151">W portalu zarządzania Azure hello na powitania **obiektu ServiceChannel** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="b3c93-151">In hello Azure Management portal, on hello **ServiceChannel** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="b3c93-153">Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="b3c93-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. <span data-ttu-id="b3c93-155">Na powitania **adresy URL i domeny obiektu ServiceChannel** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="b3c93-155">On hello **ServiceChannel Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    <span data-ttu-id="b3c93-157">a.</span><span class="sxs-lookup"><span data-stu-id="b3c93-157">a.</span></span> <span data-ttu-id="b3c93-158">W hello **identyfikator** pole tekstowe, wartość hello typu jako:`http://adfs.<domain>.com/adfs/service/trust`</span><span class="sxs-lookup"><span data-stu-id="b3c93-158">In hello **Identifier** textbox, type hello value as: `http://adfs.<domain>.com/adfs/service/trust`</span></span>

    <span data-ttu-id="b3c93-159">b.</span><span class="sxs-lookup"><span data-stu-id="b3c93-159">b.</span></span> <span data-ttu-id="b3c93-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<customer domain>.servicechannel.com/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="b3c93-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<customer domain>.servicechannel.com/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b3c93-161">Należy pamiętać, że nie są one hello wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="b3c93-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="b3c93-162">Masz tooupdate tych wartości za pomocą hello rzeczywisty identyfikator i odpowiedzi adresu URL.</span><span class="sxs-lookup"><span data-stu-id="b3c93-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="b3c93-163">W tym miejscu zalecamy możesz toouse hello unikatową wartość ciągu w hello identyfikator.</span><span class="sxs-lookup"><span data-stu-id="b3c93-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="b3c93-164">Skontaktuj się z [zespołem pomocy technicznej obiektu ServiceChannel](https://servicechannel.zendesk.com/hc/en-us) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="b3c93-164">Contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us) tooget these values.</span></span>

4. <span data-ttu-id="b3c93-165">Aplikacja obiektu ServiceChannel oczekuje potwierdzenia SAML hello w określonym formacie wymaga możesz tooadd atrybutu niestandardowego mapowania tooyour SAML tokenu atrybuty konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="b3c93-165">Your ServiceChannel application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="b3c93-166">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="b3c93-166">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="b3c93-167">**NameIdentifier (identyfikator użytkownika)** hello tylko obowiązkowe oświadczeń i hello wartość domyślna to **user.userprincipalname** , ale ta toobe zamapowana oczekuje obiektu ServiceChannel **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="b3c93-167">**NameIdentifier(User Identifier)** is hello only mandatory claim and hello default value is **user.userprincipalname** but ServiceChannel expects this toobe mapped with **user.mail**.</span></span> <span data-ttu-id="b3c93-168">Jeśli planujesz Inicjowanie obsługi użytkowników tylko w czasie tooenable, należy dodać powitania po oświadczenia, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="b3c93-168">If you are planning tooenable Just In Time user provisioning, then you should add hello following claims as shown below.</span></span> <span data-ttu-id="b3c93-169">**Rola** oświadczeń musi toobe mapowane za**user.assignedroles** zawierającą hello roli użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="b3c93-169">**Role** claim needs toobe mapped too**user.assignedroles** which contains hello role of hello user.</span></span>  

    <span data-ttu-id="b3c93-170">Może się odwoływać przewodnik obiektu ServiceChannel [tutaj](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) więcej wskazówki dotyczące oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="b3c93-170">You can refer ServiceChannel guide [here](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) for more guidance on claims.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > <span data-ttu-id="b3c93-172">Kliknij [tutaj](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow jak tooconfigure **roli** w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3c93-172">Please click [here](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow how tooconfigure **Role** in Azure AD</span></span>

5. <span data-ttu-id="b3c93-173">W **atrybuty użytkownika** kliknij **widoku i edytować wszystkie atrybuty użytkowników** i ustaw hello atrybuty.</span><span class="sxs-lookup"><span data-stu-id="b3c93-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span>

    | <span data-ttu-id="b3c93-174">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="b3c93-174">Attribute Name</span></span> | <span data-ttu-id="b3c93-175">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="b3c93-175">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="b3c93-176">Rola</span><span class="sxs-lookup"><span data-stu-id="b3c93-176">Role</span></span>| <span data-ttu-id="b3c93-177">User.assignedroles</span><span class="sxs-lookup"><span data-stu-id="b3c93-177">user.assignedroles</span></span> |

    <span data-ttu-id="b3c93-178">a.</span><span class="sxs-lookup"><span data-stu-id="b3c93-178">a.</span></span> <span data-ttu-id="b3c93-179">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3c93-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    <span data-ttu-id="b3c93-182">b.</span><span class="sxs-lookup"><span data-stu-id="b3c93-182">b.</span></span> <span data-ttu-id="b3c93-183">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="b3c93-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="b3c93-184">c.</span><span class="sxs-lookup"><span data-stu-id="b3c93-184">c.</span></span> <span data-ttu-id="b3c93-185">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="b3c93-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="b3c93-186">d.</span><span class="sxs-lookup"><span data-stu-id="b3c93-186">d.</span></span> <span data-ttu-id="b3c93-187">Kliknij przycisk **Ok**</span><span class="sxs-lookup"><span data-stu-id="b3c93-187">Click **Ok**</span></span>
    
6. <span data-ttu-id="b3c93-188">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="b3c93-188">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. <span data-ttu-id="b3c93-190">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="b3c93-190">Click **Save**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b3c93-192">Na powitania **konfiguracji obiektu ServiceChannel** kliknij **skonfigurować obiektu ServiceChannel** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="b3c93-192">On hello **ServiceChannel Configuration** section, click **Configure ServiceChannel** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="b3c93-193">Należy pamiętać, hello **identyfikator jednostka SAML** z hello **krótkimi opisami** sekcji.</span><span class="sxs-lookup"><span data-stu-id="b3c93-193">Please note hello **SAML Enitity ID** from hello **Quick Reference** section.</span></span>

9. <span data-ttu-id="b3c93-194">tooconfigure rejestracji jednokrotnej w **obiektu ServiceChannel** strony, należy pobrać hello toosend **certyfikatu (Base64)** i **identyfikator jednostki SAML** zbyt[ Zespołem pomocy technicznej obiektu ServiceChannel](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="b3c93-194">tooconfigure single sign-on on **ServiceChannel** side, you need toosend hello downloaded **certificate (Base64)** and **SAML Entity ID** too[ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us).</span></span> <span data-ttu-id="b3c93-195">One będzie skonfigurowanie tego numeru w kolejności toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML.</span><span class="sxs-lookup"><span data-stu-id="b3c93-195">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b3c93-196">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3c93-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="b3c93-197">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="b3c93-197">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="b3c93-199">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="b3c93-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3c93-200">W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="b3c93-200">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b3c93-202">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b3c93-202">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b3c93-204">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3c93-204">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b3c93-206">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="b3c93-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b3c93-208">a.</span><span class="sxs-lookup"><span data-stu-id="b3c93-208">a.</span></span> <span data-ttu-id="b3c93-209">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b3c93-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b3c93-210">b.</span><span class="sxs-lookup"><span data-stu-id="b3c93-210">b.</span></span> <span data-ttu-id="b3c93-211">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b3c93-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b3c93-212">c.</span><span class="sxs-lookup"><span data-stu-id="b3c93-212">c.</span></span> <span data-ttu-id="b3c93-213">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="b3c93-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b3c93-214">d.</span><span class="sxs-lookup"><span data-stu-id="b3c93-214">d.</span></span> <span data-ttu-id="b3c93-215">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="b3c93-215">Click **Create**.</span></span> 

### <a name="creating-a-servicechannel-test-user"></a><span data-ttu-id="b3c93-216">Tworzenie użytkownika testowego obiektu ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="b3c93-216">Creating a ServiceChannel test user</span></span>

<span data-ttu-id="b3c93-217">Aplikacja obsługuje tylko w czasie Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników zostaną utworzone w aplikacji hello automatycznie.</span><span class="sxs-lookup"><span data-stu-id="b3c93-217">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="b3c93-218">Aby Inicjowanie obsługi użytkowników pełne, skontaktuj się z [obiektu ServiceChannel zespołem pomocy technicznej](https://servicechannel.zendesk.com/hc/en-us)</span><span class="sxs-lookup"><span data-stu-id="b3c93-218">For full user provisioning, please contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us)</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="b3c93-219">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3c93-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="b3c93-220">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooServiceChannel dostępu.</span><span class="sxs-lookup"><span data-stu-id="b3c93-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooServiceChannel.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="b3c93-222">**tooassign tooServiceChannel Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="b3c93-222">**tooassign Britta Simon tooServiceChannel, perform hello following steps:**</span></span>

1. <span data-ttu-id="b3c93-223">W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="b3c93-223">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="b3c93-225">Z listy aplikacji hello wybierz **obiektu ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="b3c93-225">In hello applications list, select **ServiceChannel**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. <span data-ttu-id="b3c93-227">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="b3c93-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="b3c93-229">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="b3c93-229">Click **Add** button.</span></span> <span data-ttu-id="b3c93-230">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3c93-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="b3c93-232">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="b3c93-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b3c93-233">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3c93-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b3c93-234">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="b3c93-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b3c93-235">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="b3c93-235">Testing single sign-on</span></span>

<span data-ttu-id="b3c93-236">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="b3c93-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b3c93-237">Po kliknięciu kafelka obiektu ServiceChannel hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour obiektu ServiceChannel aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b3c93-237">When you click hello ServiceChannel tile in hello Access Panel, you should get automatically signed-on tooyour ServiceChannel application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b3c93-238">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="b3c93-238">Additional resources</span></span>

* [<span data-ttu-id="b3c93-239">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b3c93-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b3c93-240">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b3c93-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png