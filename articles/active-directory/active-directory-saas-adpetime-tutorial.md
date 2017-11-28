---
title: 'Samouczek: Integracji Azure Active Directory z ADP eTime | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i ADP eTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: a3e9f0be-19ed-4b99-a180-619e7624fc26
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 9a5c7d14a18220f8c7a5b14055c30662ecd8f14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-adp-etime"></a><span data-ttu-id="53d77-103">Samouczek: Integracji Azure Active Directory z ADP eTime</span><span class="sxs-lookup"><span data-stu-id="53d77-103">Tutorial: Azure Active Directory integration with ADP eTime</span></span>

<span data-ttu-id="53d77-104">Z tego samouczka, dowiesz się, jak eTime toointegrate ADP w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="53d77-104">In this tutorial, you learn how toointegrate ADP eTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="53d77-105">Integracja z usługą Azure AD ADP eTime zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="53d77-105">Integrating ADP eTime with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="53d77-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooADP eTime</span><span class="sxs-lookup"><span data-stu-id="53d77-106">You can control in Azure AD who has access tooADP eTime</span></span>
- <span data-ttu-id="53d77-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooADP eTime (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="53d77-107">You can enable your users tooautomatically get signed-on tooADP eTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="53d77-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="53d77-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="53d77-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="53d77-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53d77-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="53d77-110">Prerequisites</span></span>

<span data-ttu-id="53d77-111">tooconfigure integracji usługi Azure AD z ADP eTime należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="53d77-111">tooconfigure Azure AD integration with ADP eTime, you need hello following items:</span></span>

- <span data-ttu-id="53d77-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="53d77-112">An Azure AD subscription</span></span>
- <span data-ttu-id="53d77-113">ADP eTime logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="53d77-113">An ADP eTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="53d77-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="53d77-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="53d77-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="53d77-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="53d77-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="53d77-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="53d77-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="53d77-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="53d77-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="53d77-118">Scenario description</span></span>
<span data-ttu-id="53d77-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="53d77-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="53d77-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="53d77-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="53d77-121">Dodawanie ADP eTime z galerii hello</span><span class="sxs-lookup"><span data-stu-id="53d77-121">Adding ADP eTime from hello gallery</span></span>
2. <span data-ttu-id="53d77-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="53d77-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-adp-etime-from-hello-gallery"></a><span data-ttu-id="53d77-123">Dodawanie ADP eTime z galerii hello</span><span class="sxs-lookup"><span data-stu-id="53d77-123">Adding ADP eTime from hello gallery</span></span>
<span data-ttu-id="53d77-124">tooconfigure hello integracji ADP eTime do usługi Azure AD, należy eTime ADP tooadd z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="53d77-124">tooconfigure hello integration of ADP eTime into Azure AD, you need tooadd ADP eTime from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="53d77-125">**eTime tooadd ADP z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="53d77-125">**tooadd ADP eTime from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="53d77-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="53d77-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="53d77-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="53d77-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="53d77-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="53d77-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="53d77-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="53d77-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="53d77-133">W polu wyszukiwania hello wpisz **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="53d77-133">In hello search box, type **ADP eTime**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_search.png)

5. <span data-ttu-id="53d77-135">W panelu wyników hello, wybierz **ADP eTime**, a następnie kliknij przycisk **Dodaj** przycisk tooadd hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="53d77-135">In hello results panel, select **ADP eTime**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="53d77-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="53d77-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="53d77-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z eTime ADP oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="53d77-138">In this section, you configure and test Azure AD single sign-on with ADP eTime based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="53d77-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w ADP eTime jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53d77-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ADP eTime is tooa user in Azure AD.</span></span> <span data-ttu-id="53d77-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w ADP eTime musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="53d77-140">In other words, a link relationship between an Azure AD user and hello related user in ADP eTime needs toobe established.</span></span>

<span data-ttu-id="53d77-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="53d77-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ADP eTime.</span></span>

<span data-ttu-id="53d77-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z ADP eTime, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="53d77-142">tooconfigure and test Azure AD single sign-on with ADP eTime, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="53d77-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="53d77-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="53d77-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="53d77-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="53d77-145">**[Tworzenie użytkownika testowego eTime ADP](#creating-an-adp-etime-test-user)**  -toohave odpowiednikiem Simona Britta w eTime ADP, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="53d77-145">**[Creating an ADP eTime test user](#creating-an-adp-etime-test-user)** - toohave a counterpart of Britta Simon in ADP eTime that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="53d77-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="53d77-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="53d77-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="53d77-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="53d77-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="53d77-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="53d77-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji eTime ADP.</span><span class="sxs-lookup"><span data-stu-id="53d77-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ADP eTime application.</span></span>

<span data-ttu-id="53d77-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z ADP eTime wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="53d77-150">**tooconfigure Azure AD single sign-on with ADP eTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="53d77-151">W portalu Azure na powitania hello **ADP eTime** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="53d77-151">In hello Azure portal, on hello **ADP eTime** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="53d77-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="53d77-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_samlbase.png)

3. <span data-ttu-id="53d77-155">Na powitania **eTime ADP domeny i adres URL** sekcji, wykonaj powitania po kroku:</span><span class="sxs-lookup"><span data-stu-id="53d77-155">On hello **ADP eTime Domain and URLs** section, perform hello following step:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_url.png)

    <span data-ttu-id="53d77-157">a.</span><span class="sxs-lookup"><span data-stu-id="53d77-157">a.</span></span> <span data-ttu-id="53d77-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<servername>.adp.com`</span><span class="sxs-lookup"><span data-stu-id="53d77-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<servername>.adp.com`</span></span>

    <span data-ttu-id="53d77-159">b.</span><span class="sxs-lookup"><span data-stu-id="53d77-159">b.</span></span> <span data-ttu-id="53d77-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span><span class="sxs-lookup"><span data-stu-id="53d77-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<servername>.adp.com/affwebservices/public/saml2assertionconsumer`</span></span> 
 
    > [!NOTE] 
    > <span data-ttu-id="53d77-161">Wartości te nie są hello prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="53d77-161">These values are not hello real.</span></span> <span data-ttu-id="53d77-162">Zaktualizować te wartości z hello rzeczywisty adres URL odpowiedzi służący i identyfikator.</span><span class="sxs-lookup"><span data-stu-id="53d77-162">Update these values with hello actual Reply URL and Identifier.</span></span> <span data-ttu-id="53d77-163">Skontaktuj się z [zespołem pomocy technicznej eTime ADP](https://www.adp.com/contact-us/overview.aspx) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="53d77-163">Contact [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) tooget these values.</span></span>

4. <span data-ttu-id="53d77-164">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik XML hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="53d77-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_certificate.png) 

5. <span data-ttu-id="53d77-166">Witaj ADP eTime aplikacji oczekuje potwierdzenia SAML hello w określonym formacie wymaga możesz tooadd atrybutu niestandardowego mapowania tooyour SAML tokenu atrybuty konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="53d77-166">hello ADP eTime application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="53d77-167">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="53d77-167">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="53d77-168">Witaj Nazwa oświadczenia będzie zawsze **"PersonImmutableID"** i którego możemy zamapowaniu tooExtensionAttribute2, który zawiera wartość hello hello identyfikator pracownika hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="53d77-168">hello claim name will always be **"PersonImmutableID"** and hello value of which we have mapped tooExtensionAttribute2 which contains hello EmployeeID of hello user.</span></span> 

    <span data-ttu-id="53d77-169">W tym miejscu hello mapowanie użytkownika z usługi Azure AD tooADP eTime zostaną wykonane na powitania identyfikator pracownika, ale możesz mapować tej wartości różnych tooa również oparte na ustawienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="53d77-169">Here hello user mapping from Azure AD tooADP eTime will be done on hello EmployeeID but you can map this tooa different value also based on your application settings.</span></span> <span data-ttu-id="53d77-170">Pracy, dlatego należy z [zespołem pomocy technicznej eTime ADP](https://www.adp.com/contact-us/overview.aspx) toouse pierwszy hello prawidłowy identyfikator użytkownika i zmapować tę wartość z hello **"PersonImmutableID"** oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="53d77-170">So please work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) first toouse hello correct identifier of a user and map that value with hello **"PersonImmutableID"** claim.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_attribute.png)

6. <span data-ttu-id="53d77-172">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w obrazie hello i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="53d77-172">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image and perform hello following steps:</span></span>
    
    | <span data-ttu-id="53d77-173">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="53d77-173">Attribute Name</span></span> | <span data-ttu-id="53d77-174">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="53d77-174">Attribute Value</span></span> |
    | ------------------- | -------------------- |    
    | <span data-ttu-id="53d77-175">PersonImmutableID</span><span class="sxs-lookup"><span data-stu-id="53d77-175">PersonImmutableID</span></span> | <span data-ttu-id="53d77-176">User.extensionattribute2</span><span class="sxs-lookup"><span data-stu-id="53d77-176">user.extensionattribute2</span></span> |
    
    <span data-ttu-id="53d77-177">a.</span><span class="sxs-lookup"><span data-stu-id="53d77-177">a.</span></span> <span data-ttu-id="53d77-178">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="53d77-178">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adpetime-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="53d77-181">b.</span><span class="sxs-lookup"><span data-stu-id="53d77-181">b.</span></span> <span data-ttu-id="53d77-182">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="53d77-182">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>

    <span data-ttu-id="53d77-183">c.</span><span class="sxs-lookup"><span data-stu-id="53d77-183">c.</span></span> <span data-ttu-id="53d77-184">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="53d77-184">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="53d77-185">d.</span><span class="sxs-lookup"><span data-stu-id="53d77-185">d.</span></span> <span data-ttu-id="53d77-186">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="53d77-186">Click **Ok**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="53d77-187">Przed skonfigurowaniem potwierdzenia języka SAML hello należy toocontact Twojego [zespołem pomocy technicznej eTime ADP](https://www.adp.com/contact-us/overview.aspx) i zażądać hello wartość hello atrybut identyfikator unikatowy dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="53d77-187">Before you can configure hello SAML assertion, you need toocontact your [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) and request hello value of hello unique identifier attribute for your tenant.</span></span> <span data-ttu-id="53d77-188">Należy wartość tooconfigure hello oświadczenie niestandardowe dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="53d77-188">You need this value tooconfigure hello custom claim for your application.</span></span> 

7. <span data-ttu-id="53d77-189">Na powitania **eTime ADP konfiguracji** kliknij **eTime skonfigurować ADP** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="53d77-189">On hello **ADP eTime Configuration** section, click **Configure ADP eTime** tooopen **Configure sign-on** window.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_configure.png) 

8. <span data-ttu-id="53d77-191">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="53d77-191">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adpetime-tutorial/tutorial_general_400.png)

9. <span data-ttu-id="53d77-193">tooconfigure rejestracji jednokrotnej w **ADP eTime** strony, należy pobrać hello toosend **XML metadanych** za[zespołem pomocy technicznej eTime ADP](https://www.adp.com/contact-us/overview.aspx).</span><span class="sxs-lookup"><span data-stu-id="53d77-193">tooconfigure single sign-on on **ADP eTime** side, you need toosend hello downloaded **Metadata XML** too[ADP eTime support team](https://www.adp.com/contact-us/overview.aspx).</span></span> 

> [!TIP]
> <span data-ttu-id="53d77-194">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="53d77-194">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="53d77-195">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="53d77-195">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="53d77-196">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="53d77-196">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="53d77-197">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="53d77-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="53d77-198">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="53d77-198">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="53d77-200">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="53d77-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="53d77-201">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="53d77-201">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="53d77-203">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="53d77-203">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="53d77-205">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="53d77-205">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="53d77-207">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="53d77-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-adpetime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="53d77-209">a.</span><span class="sxs-lookup"><span data-stu-id="53d77-209">a.</span></span> <span data-ttu-id="53d77-210">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="53d77-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="53d77-211">b.</span><span class="sxs-lookup"><span data-stu-id="53d77-211">b.</span></span> <span data-ttu-id="53d77-212">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="53d77-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="53d77-213">c.</span><span class="sxs-lookup"><span data-stu-id="53d77-213">c.</span></span> <span data-ttu-id="53d77-214">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="53d77-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="53d77-215">d.</span><span class="sxs-lookup"><span data-stu-id="53d77-215">d.</span></span> <span data-ttu-id="53d77-216">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="53d77-216">Click **Create**.</span></span>
 
### <a name="creating-an-adp-etime-test-user"></a><span data-ttu-id="53d77-217">Tworzenie użytkownika testowego eTime ADP</span><span class="sxs-lookup"><span data-stu-id="53d77-217">Creating an ADP eTime test user</span></span>

<span data-ttu-id="53d77-218">Celem Hello w tej sekcji jest toocreate użytkownika o nazwie Simona Britta w ADP eTime.</span><span class="sxs-lookup"><span data-stu-id="53d77-218">hello objective of this section is toocreate a user called Britta Simon in ADP eTime.</span></span> <span data-ttu-id="53d77-219">Praca z [zespołem pomocy technicznej eTime ADP](https://www.adp.com/contact-us/overview.aspx) tooadd hello użytkowników w hello ADP eTime konta.</span><span class="sxs-lookup"><span data-stu-id="53d77-219">Work with [ADP eTime support team](https://www.adp.com/contact-us/overview.aspx) tooadd hello users in hello ADP eTime account.</span></span> 
   
### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="53d77-220">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="53d77-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="53d77-221">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooADP eTime.</span><span class="sxs-lookup"><span data-stu-id="53d77-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooADP eTime.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="53d77-223">**tooassign eTime tooADP Simona Britta, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="53d77-223">**tooassign Britta Simon tooADP eTime, perform hello following steps:**</span></span>

1. <span data-ttu-id="53d77-224">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="53d77-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="53d77-226">Z listy aplikacji hello wybierz **ADP eTime**.</span><span class="sxs-lookup"><span data-stu-id="53d77-226">In hello applications list, select **ADP eTime**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-adpetime-tutorial/tutorial_adpetime_app.png) 

3. <span data-ttu-id="53d77-228">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="53d77-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="53d77-230">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="53d77-230">Click **Add** button.</span></span> <span data-ttu-id="53d77-231">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="53d77-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="53d77-233">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="53d77-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="53d77-234">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="53d77-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="53d77-235">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="53d77-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="53d77-236">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="53d77-236">Testing single sign-on</span></span>

<span data-ttu-id="53d77-237">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="53d77-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="53d77-238">Po kliknięciu kafelka eTime ADP hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour ADP eTime aplikacji.</span><span class="sxs-lookup"><span data-stu-id="53d77-238">When you click hello ADP eTime tile in hello Access Panel, you should get automatically signed-on tooyour ADP eTime application.</span></span>
<span data-ttu-id="53d77-239">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="53d77-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="53d77-240">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="53d77-240">Additional resources</span></span>

* [<span data-ttu-id="53d77-241">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="53d77-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="53d77-242">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="53d77-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-adpetime-tutorial/tutorial_general_203.png

