---
title: "Samouczek: Integracji Azure Active Directory z usługi Zendesk | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i usługi Zendesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 46ccd57a4adeb810af459caaa1e592cf2b62cb8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="35295-103">Samouczek: Integracji Azure Active Directory z usługi Zendesk</span><span class="sxs-lookup"><span data-stu-id="35295-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>

<span data-ttu-id="35295-104">Z tego samouczka, dowiesz się, jak toointegrate Zendesk w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="35295-104">In this tutorial, you learn how toointegrate Zendesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="35295-105">Integrowanie usługi Zendesk z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="35295-105">Integrating Zendesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="35295-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooZendesk</span><span class="sxs-lookup"><span data-stu-id="35295-106">You can control in Azure AD who has access tooZendesk</span></span>
- <span data-ttu-id="35295-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooZendesk (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="35295-107">You can enable your users tooautomatically get signed-on tooZendesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="35295-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="35295-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="35295-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="35295-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35295-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="35295-110">Prerequisites</span></span>

<span data-ttu-id="35295-111">tooconfigure integracji z usługą Azure AD z usługi Zendesk są potrzebne hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="35295-111">tooconfigure Azure AD integration with Zendesk, you need hello following items:</span></span>

- <span data-ttu-id="35295-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="35295-112">An Azure AD subscription</span></span>
- <span data-ttu-id="35295-113">Zendesk logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="35295-113">A Zendesk single sign-on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="35295-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="35295-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="35295-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="35295-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="35295-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="35295-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="35295-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="35295-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="35295-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="35295-118">Scenario description</span></span>
<span data-ttu-id="35295-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="35295-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="35295-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="35295-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="35295-121">Dodawanie Zendesk z galerii hello</span><span class="sxs-lookup"><span data-stu-id="35295-121">Adding Zendesk from hello gallery</span></span>
2. <span data-ttu-id="35295-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="35295-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zendesk-from-hello-gallery"></a><span data-ttu-id="35295-123">Dodawanie Zendesk z galerii hello</span><span class="sxs-lookup"><span data-stu-id="35295-123">Adding Zendesk from hello gallery</span></span>
<span data-ttu-id="35295-124">tooconfigure hello integracji usługi Zendesk w usłudze Azure Active Directory, należy tooadd Zendesk z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="35295-124">tooconfigure hello integration of Zendesk into Azure AD, you need tooadd Zendesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="35295-125">**tooadd Zendesk z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="35295-125">**tooadd Zendesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="35295-126">W hello  **[Azure Portal](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="35295-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="35295-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="35295-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="35295-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="35295-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="35295-131">Kliknij przycisk **nowej aplikacji** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="35295-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="35295-133">W polu wyszukiwania hello wpisz **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="35295-133">In hello search box, type **Zendesk**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. <span data-ttu-id="35295-135">W panelu wyników hello zaznacz **Zendesk**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="35295-135">In hello results panel, select **Zendesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="35295-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="35295-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="35295-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi Zendesk w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="35295-138">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="35295-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w Zendesk jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="35295-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zendesk is tooa user in Azure AD.</span></span> <span data-ttu-id="35295-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w Zendesk musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="35295-140">In other words, a link relationship between an Azure AD user and hello related user in Zendesk needs toobe established.</span></span>

<span data-ttu-id="35295-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w Zendesk.</span><span class="sxs-lookup"><span data-stu-id="35295-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zendesk.</span></span>

<span data-ttu-id="35295-142">tooconfigure i test usługi Azure AD rejestracji jednokrotnej z usługi Zendesk są potrzebne hello toocomplete po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="35295-142">tooconfigure and test Azure AD single sign-on with Zendesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="35295-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="35295-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="35295-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="35295-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="35295-145">**[Tworzenie użytkownika testowego Zendesk](#creating-a-zendesk-test-user)**  -toohave odpowiednikiem Simona Britta w Zendesk, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="35295-145">**[Creating a Zendesk test user](#creating-a-zendesk-test-user)** - toohave a counterpart of Britta Simon in Zendesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="35295-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="35295-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="35295-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="35295-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="35295-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="35295-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="35295-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować rejestracji jednokrotnej w aplikacji Zendesk.</span><span class="sxs-lookup"><span data-stu-id="35295-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zendesk application.</span></span>

<span data-ttu-id="35295-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z usługi Zendesk, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="35295-150">**tooconfigure Azure AD single sign-on with Zendesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="35295-151">W portalu Azure na powitania hello **Zendesk** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="35295-151">In hello Azure portal, on hello **Zendesk** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="35295-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="35295-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. <span data-ttu-id="35295-155">Na powitania **Zendesk domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="35295-155">On hello **Zendesk Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    <span data-ttu-id="35295-157">a.</span><span class="sxs-lookup"><span data-stu-id="35295-157">a.</span></span> <span data-ttu-id="35295-158">W hello **adres URL logowania** pole tekstowe, wartość hello typu przy użyciu hello następującego wzorca:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="35295-158">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<subdomain>.zendesk.com`</span></span>

    <span data-ttu-id="35295-159">b.</span><span class="sxs-lookup"><span data-stu-id="35295-159">b.</span></span> <span data-ttu-id="35295-160">W hello **identyfikator** pole tekstowe, wartość hello typu przy użyciu hello następującego wzorca:`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="35295-160">In hello **Identifier** textbox, type hello value using hello following pattern: `https://<subdomain>.zendesk.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="35295-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="35295-161">These values are not real.</span></span> <span data-ttu-id="35295-162">Witaj rzeczywisty adres URL logowania i adres URL identyfikatora, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="35295-162">Update these values with hello actual Sign-on URL and Identifier URL.</span></span> <span data-ttu-id="35295-163">Skontaktuj się z [zespołem pomocy technicznej usługi Zendesk](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="35295-163">Contact [Zendesk support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget these values.</span></span> 

4. <span data-ttu-id="35295-164">Zendesk oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="35295-164">Zendesk expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="35295-165">Nie obowiązkowych atrybutów SAML, ale Opcjonalnie można dodać atrybutu z **atrybuty użytkownika** sekcji przez następujące hello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="35295-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following hello below steps:</span></span> 

     ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    <span data-ttu-id="35295-167">a.</span><span class="sxs-lookup"><span data-stu-id="35295-167">a.</span></span> <span data-ttu-id="35295-168">Kliknij przycisk hello **wyświetlanie i edytowanie wszystkich innych atrybutów hello** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="35295-168">Click hello **View and edit all hello other attributes** check box.</span></span>
     
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    <span data-ttu-id="35295-170">b.</span><span class="sxs-lookup"><span data-stu-id="35295-170">b.</span></span> <span data-ttu-id="35295-171">Kliknij przycisk hello **Dodawanie atrybutu** tooopen **Dodaj atrybut** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="35295-171">Click hello **Add Attribute** tooopen **Add attribute** dialog.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="35295-173">c.</span><span class="sxs-lookup"><span data-stu-id="35295-173">c.</span></span> <span data-ttu-id="35295-174">W hello **nazwa** pole tekstowe, nazwa atrybutu typu hello (na przykład **emailaddress**).</span><span class="sxs-lookup"><span data-stu-id="35295-174">In hello **Name** textbox, type hello attribute name (for example **emailaddress**).</span></span>
    
    <span data-ttu-id="35295-175">d.</span><span class="sxs-lookup"><span data-stu-id="35295-175">d.</span></span> <span data-ttu-id="35295-176">Z hello **wartość** listy, wybierz hello wartość atrybutu (jako **user.mail**).</span><span class="sxs-lookup"><span data-stu-id="35295-176">From hello **Value** list, select hello attribute value (as **user.mail**).</span></span>
    
    <span data-ttu-id="35295-177">e.</span><span class="sxs-lookup"><span data-stu-id="35295-177">e.</span></span> <span data-ttu-id="35295-178">Kliknij przycisk **Ok**</span><span class="sxs-lookup"><span data-stu-id="35295-178">Click **Ok**</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="35295-179">Możesz użyć atrybuty tooadd atrybuty rozszerzenia, które nie są dostępne w usłudze Azure AD domyślnie.</span><span class="sxs-lookup"><span data-stu-id="35295-179">You use extension attributes tooadd attributes that are not in Azure AD by default.</span></span> <span data-ttu-id="35295-180">Kliknij przycisk [atrybutów użytkowników, które można ustawić w SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget hello pełną listę SAML atrybuty, które **Zendesk** akceptuje.</span><span class="sxs-lookup"><span data-stu-id="35295-180">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget hello complete list of SAML attributes that **Zendesk** accepts.</span></span> 

5. <span data-ttu-id="35295-181">Na powitania **certyfikat podpisywania SAML** hello kopiowania, sekcji **odcisk PALCA** wartości certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="35295-181">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. <span data-ttu-id="35295-183">Na powitania **konfiguracji usługi Zendesk** kliknij **skonfigurować Zendesk** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="35295-183">On hello **Zendesk Configuration** section, click **Configure Zendesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="35295-184">Kopiuj hello **Sign-Out adresu URL i SAML pojedynczy znak na adres URL usługi** z hello **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="35295-184">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. <span data-ttu-id="35295-186">W oknie przeglądarki innej witryny sieci web Zaloguj się do witryny firmy Zendesk jako administrator.</span><span class="sxs-lookup"><span data-stu-id="35295-186">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

8. <span data-ttu-id="35295-187">Kliknij przycisk **Admin**.</span><span class="sxs-lookup"><span data-stu-id="35295-187">Click **Admin**.</span></span>

9. <span data-ttu-id="35295-188">W okienku nawigacji po lewej stronie powitania kliknij **ustawienia**, a następnie kliknij przycisk **zabezpieczeń**.</span><span class="sxs-lookup"><span data-stu-id="35295-188">In hello left navigation pane, click **Settings**, and then click **Security**.</span></span>

10. <span data-ttu-id="35295-189">Na powitania **zabezpieczeń** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="35295-189">On hello **Security** page, perform hello following steps:</span></span> 
   
     <span data-ttu-id="35295-190">![Zabezpieczenia](./media/active-directory-saas-zendesk-tutorial/ic773089.png "zabezpieczeń")</span><span class="sxs-lookup"><span data-stu-id="35295-190">![Security](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Security")</span></span>

    <span data-ttu-id="35295-191">![Logowanie jednokrotne](./media/active-directory-saas-zendesk-tutorial/ic773090.png "logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="35295-191">![Single sign-on](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single sign-on")</span></span>

     <span data-ttu-id="35295-192">a.</span><span class="sxs-lookup"><span data-stu-id="35295-192">a.</span></span> <span data-ttu-id="35295-193">Kliknij przycisk hello **Admin & agentów** kartę.</span><span class="sxs-lookup"><span data-stu-id="35295-193">Click hello **Admin & Agents** tab.</span></span>

     <span data-ttu-id="35295-194">b.</span><span class="sxs-lookup"><span data-stu-id="35295-194">b.</span></span> <span data-ttu-id="35295-195">Wybierz **logowanie jednokrotne (SSO) oraz SAML**, a następnie wybierz **SAML**.</span><span class="sxs-lookup"><span data-stu-id="35295-195">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

     <span data-ttu-id="35295-196">c.</span><span class="sxs-lookup"><span data-stu-id="35295-196">c.</span></span> <span data-ttu-id="35295-197">W **adres URL logowania jednokrotnego SAML** pole tekstowe, Wklej wartość hello **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="35295-197">In **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

     <span data-ttu-id="35295-198">d.</span><span class="sxs-lookup"><span data-stu-id="35295-198">d.</span></span> <span data-ttu-id="35295-199">W **zdalnego adresu URL wylogowania** pole tekstowe, Wklej wartość hello **Sign-Out URL** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="35295-199">In **Remote Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
        
     <span data-ttu-id="35295-200">e.</span><span class="sxs-lookup"><span data-stu-id="35295-200">e.</span></span> <span data-ttu-id="35295-201">W **odcisk palca certyfikatu** pole tekstowe, Wklej hello **odcisk palca** wartość certyfikatów, które zostały skopiowane z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="35295-201">In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="35295-202">f.</span><span class="sxs-lookup"><span data-stu-id="35295-202">f.</span></span> <span data-ttu-id="35295-203">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="35295-203">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="35295-204">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="35295-204">Creating an Azure AD test user</span></span>
<span data-ttu-id="35295-205">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="35295-205">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="35295-207">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="35295-207">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="35295-208">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="35295-208">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="35295-210">toodisplay hello listę użytkowników przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="35295-210">toodisplay hello list of users go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="35295-212">U góry okna dialogowego hello hello, kliknij przycisk **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="35295-212">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="35295-214">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="35295-214">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="35295-216">a.</span><span class="sxs-lookup"><span data-stu-id="35295-216">a.</span></span> <span data-ttu-id="35295-217">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="35295-217">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="35295-218">b.</span><span class="sxs-lookup"><span data-stu-id="35295-218">b.</span></span> <span data-ttu-id="35295-219">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="35295-219">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="35295-220">c.</span><span class="sxs-lookup"><span data-stu-id="35295-220">c.</span></span> <span data-ttu-id="35295-221">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="35295-221">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="35295-222">d.</span><span class="sxs-lookup"><span data-stu-id="35295-222">d.</span></span> <span data-ttu-id="35295-223">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="35295-223">Click **Create**.</span></span> 

### <a name="creating-a-zendesk-test-user"></a><span data-ttu-id="35295-224">Tworzenie użytkownika testowego Zendesk</span><span class="sxs-lookup"><span data-stu-id="35295-224">Creating a Zendesk test user</span></span>

<span data-ttu-id="35295-225">tooenable usługi Azure AD użytkownicy toolog do **Zendesk**, muszą mieć przydzielone do **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="35295-225">tooenable Azure AD users toolog into **Zendesk**, they must be provisioned into **Zendesk**.</span></span>  
<span data-ttu-id="35295-226">W zależności od roli hello przypisane w aplikacji hello jego hello oczekiwane zachowanie:</span><span class="sxs-lookup"><span data-stu-id="35295-226">Depending on hello role assigned in hello apps, it's hello expected behavior:</span></span>

 1. <span data-ttu-id="35295-227">**Użytkownik końcowy** konta są automatycznie konfigurowani podczas logowania.</span><span class="sxs-lookup"><span data-stu-id="35295-227">**End-user** accounts are automatically provisioned when signing in.</span></span>
 2. <span data-ttu-id="35295-228">**Agent** i **Admin** konta potrzebują toobe ręcznie udostępniane w **Zendesk** przed zarejestrowaniem się.</span><span class="sxs-lookup"><span data-stu-id="35295-228">**Agent** and **Admin** accounts need toobe manually provisioned in **Zendesk** before signing in.</span></span>
 
<span data-ttu-id="35295-229">**tooprovision konta użytkownika, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="35295-229">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="35295-230">Zaloguj się za tooyour **Zendesk** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="35295-230">Log in tooyour **Zendesk** tenant.</span></span>

2. <span data-ttu-id="35295-231">Wybierz hello **listy odbiorców** kartę.</span><span class="sxs-lookup"><span data-stu-id="35295-231">Select hello **Customer List** tab.</span></span>

3. <span data-ttu-id="35295-232">Wybierz hello **użytkownika** , a następnie kliknij pozycję **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="35295-232">Select hello **User** tab, and click **Add**.</span></span>
   
    <span data-ttu-id="35295-233">![Dodaj użytkownika](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Dodaj użytkownika")</span><span class="sxs-lookup"><span data-stu-id="35295-233">![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")</span></span>
4. <span data-ttu-id="35295-234">Wpisz adres e-mail hello istniejącego konta usługi Azure AD tooprovision, a następnie kliknij przycisk **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="35295-234">Type hello email address of an existing Azure AD account you want tooprovision, and then click **Save**.</span></span>
   
    <span data-ttu-id="35295-235">![Nowy użytkownik](./media/active-directory-saas-zendesk-tutorial/ic773633.png "nowego użytkownika")</span><span class="sxs-lookup"><span data-stu-id="35295-235">![New user](./media/active-directory-saas-zendesk-tutorial/ic773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="35295-236">Możesz użyć innych Zendesk użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Zendesk tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="35295-236">You can use any other Zendesk user account creation tools or APIs provided by Zendesk tooprovision AAD user accounts.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="35295-237">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="35295-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="35295-238">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooZendesk.</span><span class="sxs-lookup"><span data-stu-id="35295-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZendesk.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="35295-240">**tooassign tooZendesk Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="35295-240">**tooassign Britta Simon tooZendesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="35295-241">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="35295-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="35295-243">Z listy aplikacji hello wybierz **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="35295-243">In hello applications list, select **Zendesk**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. <span data-ttu-id="35295-245">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="35295-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="35295-247">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="35295-247">Click **Add** button.</span></span> <span data-ttu-id="35295-248">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="35295-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="35295-250">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="35295-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="35295-251">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="35295-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="35295-252">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="35295-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="35295-253">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="35295-253">Testing single sign-on</span></span>

<span data-ttu-id="35295-254">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="35295-254">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="35295-255">Po kliknięciu kafelka Zendesk hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour Zendesk aplikacji.</span><span class="sxs-lookup"><span data-stu-id="35295-255">When you click hello Zendesk tile in hello Access Panel, you should get automatically signed-on tooyour Zendesk application.</span></span>
<span data-ttu-id="35295-256">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="35295-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="35295-257">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="35295-257">Additional resources</span></span>

* [<span data-ttu-id="35295-258">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="35295-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="35295-259">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="35295-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
