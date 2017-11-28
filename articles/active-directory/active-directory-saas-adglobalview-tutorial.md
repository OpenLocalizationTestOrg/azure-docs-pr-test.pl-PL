---
title: 'Samouczek: Integracji Azure Active Directory z ADP Globalview | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i ADP Globalview."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ffb6464f-714d-41a9-869a-2b7e5ae9f125
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: aee2d56f05b486d12facbc41c9503455094604ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-globalview"></a><span data-ttu-id="d9994-103">Samouczek: Integracji Azure Active Directory z ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="d9994-103">Tutorial: Azure Active Directory integration with ADP Globalview</span></span>

<span data-ttu-id="d9994-104">Z tego samouczka, dowiesz się, jak toointegrate ADP Globalview w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d9994-104">In this tutorial, you learn how toointegrate ADP Globalview with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d9994-105">Integracja z usługą Azure AD ADP Globalview zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d9994-105">Integrating ADP Globalview with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="d9994-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooADP Globalview</span><span class="sxs-lookup"><span data-stu-id="d9994-106">You can control in Azure AD who has access tooADP Globalview</span></span>
- <span data-ttu-id="d9994-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooADP Globalview (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9994-107">You can enable your users tooautomatically get signed-on tooADP Globalview (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d9994-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d9994-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="d9994-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d9994-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9994-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d9994-110">Prerequisites</span></span>

<span data-ttu-id="d9994-111">tooconfigure integracji usługi Azure AD z ADP Globalview należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d9994-111">tooconfigure Azure AD integration with ADP Globalview, you need hello following items:</span></span>

- <span data-ttu-id="d9994-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9994-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d9994-113">ADP Globalview logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d9994-113">An ADP Globalview single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d9994-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d9994-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d9994-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d9994-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d9994-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d9994-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d9994-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d9994-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d9994-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d9994-118">Scenario description</span></span>
<span data-ttu-id="d9994-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d9994-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d9994-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d9994-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d9994-121">Dodawanie ADP Globalview z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d9994-121">Adding ADP Globalview from hello gallery</span></span>
2. <span data-ttu-id="d9994-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d9994-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-globalview-from-hello-gallery"></a><span data-ttu-id="d9994-123">Dodawanie ADP Globalview z galerii hello</span><span class="sxs-lookup"><span data-stu-id="d9994-123">Adding ADP Globalview from hello gallery</span></span>
<span data-ttu-id="d9994-124">tooconfigure hello integracji ADP Globalview do usługi Azure AD, należy tooadd ADP Globalview z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d9994-124">tooconfigure hello integration of ADP Globalview into Azure AD, you need tooadd ADP Globalview from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="d9994-125">**tooadd ADP Globalview z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d9994-125">**tooadd ADP Globalview from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9994-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d9994-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="d9994-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="d9994-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="d9994-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d9994-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="d9994-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d9994-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="d9994-133">W polu wyszukiwania hello wpisz **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="d9994-133">In hello search box, type **ADP Globalview**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_search.png)

5. <span data-ttu-id="d9994-135">W panelu wyników hello, wybierz **ADP Globalview**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d9994-135">In hello results panel, select **ADP Globalview**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d9994-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="d9994-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d9994-138">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z ADP Globalview oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="d9994-138">In this section, you configure and test Azure AD single sign-on with ADP Globalview based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d9994-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w ADP Globalview jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d9994-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ADP Globalview is tooa user in Azure AD.</span></span> <span data-ttu-id="d9994-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w ADP Globalview musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="d9994-140">In other words, a link relationship between an Azure AD user and hello related user in ADP Globalview needs toobe established.</span></span>

<span data-ttu-id="d9994-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="d9994-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ADP Globalview.</span></span>

<span data-ttu-id="d9994-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z ADP Globalview, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="d9994-142">tooconfigure and test Azure AD single sign-on with ADP Globalview, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="d9994-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d9994-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="d9994-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d9994-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d9994-145">**[Tworzenie użytkownika testowego ADP Globalview](#creating-an-adp-globalview-test-user)**  -toohave odpowiednikiem Simona Britta w ADP Globalview, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d9994-145">**[Creating an ADP Globalview test user](#creating-an-adp-globalview-test-user)** - toohave a counterpart of Britta Simon in ADP Globalview that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="d9994-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d9994-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d9994-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="d9994-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d9994-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d9994-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d9994-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji ADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="d9994-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ADP Globalview application.</span></span>

<span data-ttu-id="d9994-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z ADP Globalview wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="d9994-150">**tooconfigure Azure AD single sign-on with ADP Globalview, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9994-151">W portalu Azure na powitania hello **ADP Globalview** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="d9994-151">In hello Azure portal, on hello **ADP Globalview** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="d9994-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d9994-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_samlbase.png)

3. <span data-ttu-id="d9994-155">Na powitania **ADP Globalview domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="d9994-155">On hello **ADP Globalview Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_url.png)

     <span data-ttu-id="d9994-157">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca: `https://<subdomain>.globalview.adp.com/federate` lub`https://<subdomain>.globalview.adp.com/federate2`</span><span class="sxs-lookup"><span data-stu-id="d9994-157">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.globalview.adp.com/federate` or `https://<subdomain>.globalview.adp.com/federate2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d9994-158">wartość Hello nie jest prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="d9994-158">hello value is not real.</span></span> <span data-ttu-id="d9994-159">Zaktualizuj wartość hello z hello rzeczywisty identyfikator.</span><span class="sxs-lookup"><span data-stu-id="d9994-159">Update hello value with hello actual Identifier.</span></span> <span data-ttu-id="d9994-160">Skontaktuj się z [Obsługa ADP Globalview](https://www.adp.com/contact-us/overview.aspx) tooget hello wartość.</span><span class="sxs-lookup"><span data-stu-id="d9994-160">Contact [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) tooget hello value.</span></span>
 
4. <span data-ttu-id="d9994-161">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="d9994-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_certificate.png) 

5. <span data-ttu-id="d9994-163">Hello aplikacji ADP GlobalView oczekuje potwierdzenia SAML hello w określonym formacie wymaga możesz tooadd atrybutu niestandardowego mapowania tooyour SAML tokenu atrybuty konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d9994-163">hello ADP GlobalView application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> 

6. <span data-ttu-id="d9994-164">powitania po zrzut ekranu przedstawia przykład dla niego.</span><span class="sxs-lookup"><span data-stu-id="d9994-164">hello following screenshot shows an example for it.</span></span> <span data-ttu-id="d9994-165">Witaj oświadczenia nazwy zawsze być **"PersonImmutableID"** i którego możemy zamapowaniu tooExtensionAttribute2, który zawiera wartość hello hello identyfikator pracownika hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="d9994-165">hello claim names always be **"PersonImmutableID"** and hello value of which we have mapped tooExtensionAttribute2, which contains hello EmployeeID of hello user.</span></span> <span data-ttu-id="d9994-166">W tym miejscu hello mapowanie użytkownika z usługi Azure AD tooADP GlobalView jest wykonywana na powitania identyfikator pracownika, ale można mapować inną wartość tooa również oparte na ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d9994-166">Here hello user mapping from Azure AD tooADP GlobalView is done on hello EmployeeID but you can map it tooa different value also based on your application settings.</span></span> <span data-ttu-id="d9994-167">Możesz pracować z hello ADP GlobalView zespołu pierwszy toouse hello prawidłowy identyfikator użytkownika i zmapować tę wartość z hello **"PersonImmutableID"** oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="d9994-167">You can work with hello ADP GlobalView team first toouse hello correct identifier of a user and map that value with hello **"PersonImmutableID"** claim.</span></span> <span data-ttu-id="d9994-168">Można również mapować hello poczty E-mail i UserID oświadczeń jak pokazano na rysunku hello.</span><span class="sxs-lookup"><span data-stu-id="d9994-168">You can also map hello Email and UserID claim as shown in hello picture.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_attribute.png)

7. <span data-ttu-id="d9994-170">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie hello i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d9994-170">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="d9994-171">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="d9994-171">Attribute Name</span></span> | <span data-ttu-id="d9994-172">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="d9994-172">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="d9994-173">personalimmutableid</span><span class="sxs-lookup"><span data-stu-id="d9994-173">personalimmutableid</span></span> | <span data-ttu-id="d9994-174">User.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="d9994-174">user.extensionattribute2</span></span> |
    | <span data-ttu-id="d9994-175">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="d9994-175">email</span></span>               | <span data-ttu-id="d9994-176">User.mail</span><span class="sxs-lookup"><span data-stu-id="d9994-176">user.mail</span></span> |
    | <span data-ttu-id="d9994-177">Nazwa użytkownika</span><span class="sxs-lookup"><span data-stu-id="d9994-177">userid</span></span>              | <span data-ttu-id="d9994-178">User.userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="d9994-178">user.userprincipalname</span></span>|
    
    <span data-ttu-id="d9994-179">a.</span><span class="sxs-lookup"><span data-stu-id="d9994-179">a.</span></span> <span data-ttu-id="d9994-180">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d9994-180">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adglobalview-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="d9994-183">b.</span><span class="sxs-lookup"><span data-stu-id="d9994-183">b.</span></span> <span data-ttu-id="d9994-184">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="d9994-184">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="d9994-185">c.</span><span class="sxs-lookup"><span data-stu-id="d9994-185">c.</span></span> <span data-ttu-id="d9994-186">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="d9994-186">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="d9994-187">d.</span><span class="sxs-lookup"><span data-stu-id="d9994-187">d.</span></span> <span data-ttu-id="d9994-188">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="d9994-188">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d9994-189">Przed skonfigurowaniem potwierdzenia języka SAML hello należy toocontact Twojego [Obsługa ADP Globalview](https://www.adp.com/contact-us/overview.aspx) i zażądać hello wartość hello atrybut identyfikator unikatowy dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="d9994-189">Before you can configure hello SAML assertion, you need toocontact your [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="d9994-190">Należy wartość tooconfigure hello oświadczenie niestandardowe dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d9994-190">You need this value tooconfigure hello custom claim for your application.</span></span> 

8. <span data-ttu-id="d9994-191">Na powitania **ADP Globalview konfiguracji** kliknij **skonfigurować ADP Globalview** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="d9994-191">On hello **ADP Globalview Configuration** section, click **Configure ADP Globalview** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="d9994-192">Kopiuj hello **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="d9994-192">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_configure.png) 

9. <span data-ttu-id="d9994-194">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d9994-194">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adglobalview-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="d9994-196">tooconfigure rejestracji jednokrotnej w **ADP Globalview** strony, należy pobrać hello toosend **certyfikatu (Base64)**, **Sign-Out adres URL, identyfikator jednostki SAML i SAML pojedynczy znak na adres URL usługi** za[Obsługa ADP Globalview](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="d9994-196">tooconfigure single sign-on on **ADP Globalview** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[ADP Globalview support](https://www.adp.com/contact-us/overview.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="d9994-197">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="d9994-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="d9994-198">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="d9994-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="d9994-199">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="d9994-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d9994-200">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9994-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="d9994-201">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="d9994-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="d9994-203">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d9994-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9994-204">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="d9994-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_01.png) 

2.  <span data-ttu-id="d9994-206">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="d9994-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d9994-208">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d9994-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d9994-210">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="d9994-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adglobalview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d9994-212">a.</span><span class="sxs-lookup"><span data-stu-id="d9994-212">a.</span></span> <span data-ttu-id="d9994-213">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d9994-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d9994-214">b.</span><span class="sxs-lookup"><span data-stu-id="d9994-214">b.</span></span> <span data-ttu-id="d9994-215">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d9994-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d9994-216">c.</span><span class="sxs-lookup"><span data-stu-id="d9994-216">c.</span></span> <span data-ttu-id="d9994-217">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="d9994-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="d9994-218">d.</span><span class="sxs-lookup"><span data-stu-id="d9994-218">d.</span></span> <span data-ttu-id="d9994-219">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="d9994-219">Click **Create**.</span></span>
 
### <a name="creating-an-adp-globalview-test-user"></a><span data-ttu-id="d9994-220">Tworzenie użytkownika testowego ADP Globalview</span><span class="sxs-lookup"><span data-stu-id="d9994-220">Creating an ADP Globalview test user</span></span>

<span data-ttu-id="d9994-221">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w ADP GlobalView.</span><span class="sxs-lookup"><span data-stu-id="d9994-221">hello objective of this section is toocreate a user called Britta Simon in ADP GlobalView.</span></span> <span data-ttu-id="d9994-222">Praca z [Obsługa ADP Globalview](https://www.adp.com/contact-us/overview.aspx) tooadd hello użytkowników w hello ADP GlobalView konta.</span><span class="sxs-lookup"><span data-stu-id="d9994-222">Work with [ADP Globalview support](https://www.adp.com/contact-us/overview.aspx) tooadd hello users in hello ADP GlobalView account.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="d9994-223">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="d9994-223">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="d9994-224">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooADP Globalview.</span><span class="sxs-lookup"><span data-stu-id="d9994-224">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooADP Globalview.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="d9994-226">**tooassign tooADP Simona Britta Globalview, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="d9994-226">**tooassign Britta Simon tooADP Globalview, perform hello following steps:**</span></span>

1. <span data-ttu-id="d9994-227">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="d9994-227">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d9994-229">Z listy aplikacji hello wybierz **ADP Globalview**.</span><span class="sxs-lookup"><span data-stu-id="d9994-229">In hello applications list, select **ADP Globalview**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adglobalview-tutorial/tutorial_adpglobalview_app.png) 

3. <span data-ttu-id="d9994-231">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="d9994-231">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="d9994-233">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="d9994-233">Click **Add** button.</span></span> <span data-ttu-id="d9994-234">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d9994-234">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="d9994-236">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="d9994-236">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="d9994-237">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d9994-237">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d9994-238">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d9994-238">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d9994-239">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d9994-239">Testing single sign-on</span></span>

<span data-ttu-id="d9994-240">Celem Hello w tej sekcji jest tootest programu Azure AD SSO konfiguracji przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d9994-240">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>  

<span data-ttu-id="d9994-241">Po kliknięciu hello ADP GlobalView kafelka w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour ADP GlobalView aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d9994-241">When you click hello ADP GlobalView tile in hello Access Panel, you should get automatically signed-on tooyour ADP GlobalView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d9994-242">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d9994-242">Additional resources</span></span>

* [<span data-ttu-id="d9994-243">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d9994-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d9994-244">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d9994-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adglobalview-tutorial/tutorial_general_203.png

