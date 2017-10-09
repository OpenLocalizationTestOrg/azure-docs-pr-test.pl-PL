---
title: 'Samouczek: Integracji Azure Active Directory z FilesAnywhere | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i FilesAnywhere."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28acce3e-22a0-4a37-8b66-6e518d777350
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: jeedes
ms.openlocfilehash: 376364a5c75f8d069ea6390c58586acb378cd8b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filesanywhere"></a><span data-ttu-id="90201-103">Samouczek: Integracji Azure Active Directory z FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="90201-103">Tutorial: Azure Active Directory integration with FilesAnywhere</span></span>

<span data-ttu-id="90201-104">Z tego samouczka, dowiesz się, jak toointegrate FilesAnywhere w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="90201-104">In this tutorial, you learn how toointegrate FilesAnywhere with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="90201-105">Integracja z usługą Azure AD FilesAnywhere zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="90201-105">Integrating FilesAnywhere with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="90201-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooFilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="90201-106">You can control in Azure AD who has access tooFilesAnywhere</span></span>
- <span data-ttu-id="90201-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooFilesAnywhere (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="90201-107">You can enable your users tooautomatically get signed-on tooFilesAnywhere (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="90201-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu zarządzania Azure</span><span class="sxs-lookup"><span data-stu-id="90201-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="90201-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="90201-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90201-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="90201-110">Prerequisites</span></span>

<span data-ttu-id="90201-111">tooconfigure integracji z usługą Azure AD z FilesAnywhere należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="90201-111">tooconfigure Azure AD integration with FilesAnywhere, you need hello following items:</span></span>

- <span data-ttu-id="90201-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="90201-112">An Azure AD subscription</span></span>
- <span data-ttu-id="90201-113">FilesAnywhere jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="90201-113">A FilesAnywhere single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="90201-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="90201-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="90201-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="90201-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="90201-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="90201-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="90201-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="90201-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="90201-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="90201-118">Scenario description</span></span>
<span data-ttu-id="90201-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="90201-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="90201-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="90201-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="90201-121">Dodawanie FilesAnywhere z galerii hello</span><span class="sxs-lookup"><span data-stu-id="90201-121">Adding FilesAnywhere from hello gallery</span></span>
2. <span data-ttu-id="90201-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="90201-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-filesanywhere-from-hello-gallery"></a><span data-ttu-id="90201-123">Dodawanie FilesAnywhere z galerii hello</span><span class="sxs-lookup"><span data-stu-id="90201-123">Adding FilesAnywhere from hello gallery</span></span>
<span data-ttu-id="90201-124">tooconfigure hello integracji FilesAnywhere do usługi Azure AD, należy tooadd FilesAnywhere z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="90201-124">tooconfigure hello integration of FilesAnywhere into Azure AD, you need tooadd FilesAnywhere from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="90201-125">**tooadd FilesAnywhere z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="90201-125">**tooadd FilesAnywhere from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="90201-126">W hello  **[portalu zarządzania Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="90201-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="90201-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="90201-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="90201-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="90201-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="90201-131">Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="90201-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="90201-133">W polu wyszukiwania hello wpisz **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="90201-133">In hello search box, type **FilesAnywhere**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_search.png)

5. <span data-ttu-id="90201-135">W panelu wyników hello zaznacz **FilesAnywhere**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="90201-135">In hello results panel, select **FilesAnywhere**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_addfromgallery.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="90201-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="90201-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="90201-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z FilesAnywhere w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="90201-138">In this section, you configure and test Azure AD single sign-on with FilesAnywhere based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="90201-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w FilesAnywhere jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90201-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FilesAnywhere is tooa user in Azure AD.</span></span> <span data-ttu-id="90201-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w FilesAnywhere musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="90201-140">In other words, a link relationship between an Azure AD user and hello related user in FilesAnywhere needs toobe established.</span></span>

<span data-ttu-id="90201-141">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="90201-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in FilesAnywhere.</span></span>

<span data-ttu-id="90201-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z FilesAnywhere, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="90201-142">tooconfigure and test Azure AD single sign-on with FilesAnywhere, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="90201-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="90201-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="90201-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="90201-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="90201-145">**[Tworzenie użytkownika testowego FilesAnywhere](#creating-a-filesanywhere-test-user)**  -toohave odpowiednikiem Simona Britta w FilesAnywhere, że jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="90201-145">**[Creating a FilesAnywhere test user](#creating-a-filesanywhere-test-user)** - toohave a counterpart of Britta Simon in FilesAnywhere that is linked toohello Azure AD representation of her.</span></span>
3. <span data-ttu-id="90201-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="90201-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
4. <span data-ttu-id="90201-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="90201-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="90201-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="90201-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="90201-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne w aplikacji FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="90201-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your FilesAnywhere application.</span></span>

<span data-ttu-id="90201-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z FilesAnywhere, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="90201-150">**tooconfigure Azure AD single sign-on with FilesAnywhere, perform hello following steps:**</span></span>

1. <span data-ttu-id="90201-151">W portalu zarządzania Azure hello na powitania **FilesAnywhere** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="90201-151">In hello Azure Management portal, on hello **FilesAnywhere** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="90201-153">Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="90201-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_samlbase.png)

3. <span data-ttu-id="90201-155">Na powitania **FilesAnywhere domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **IDP zainicjował tryb**:</span><span class="sxs-lookup"><span data-stu-id="90201-155">On hello **FilesAnywhere Domain and URLs** section, If you wish tooconfigure hello application in **IDP initiated mode**:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url.png)
    
    <span data-ttu-id="90201-157">a.</span><span class="sxs-lookup"><span data-stu-id="90201-157">a.</span></span> <span data-ttu-id="90201-158">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span><span class="sxs-lookup"><span data-stu-id="90201-158">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.filesanywhere.com/saml20.aspx?c=215`</span></span>
> [!NOTE]
> <span data-ttu-id="90201-159">Należy pamiętać, ta wartość hello **215** jest **clientid** i jest tylko przykładowe.</span><span class="sxs-lookup"><span data-stu-id="90201-159">Please note that hello value **215** is a **clientid** and is just an example.</span></span> <span data-ttu-id="90201-160">Należy tooreplace za pomocą hello clientid rzeczywiste wartości.</span><span class="sxs-lookup"><span data-stu-id="90201-160">You need tooreplace it with hello actual clientid value.</span></span>

4. <span data-ttu-id="90201-161">Na powitania **FilesAnywhere domeny i adres URL** sekcji, jeśli chcesz, aby aplikacja hello tooconfigure w **SP zainicjował tryb**, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="90201-161">On hello **FilesAnywhere Domain and URLs** section, If you wish tooconfigure hello application in **SP initiated mode**, perform hello following steps:</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_url1.png)

    <span data-ttu-id="90201-163">a.</span><span class="sxs-lookup"><span data-stu-id="90201-163">a.</span></span> <span data-ttu-id="90201-164">Polecenie hello **Pokaż zaawansowane ustawienia adresu URL** opcji</span><span class="sxs-lookup"><span data-stu-id="90201-164">Click on hello **Show advanced URL settings** option</span></span>

    <span data-ttu-id="90201-165">b.</span><span class="sxs-lookup"><span data-stu-id="90201-165">b.</span></span> <span data-ttu-id="90201-166">W hello **na adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<sub domain>.filesanywhere.com/`</span><span class="sxs-lookup"><span data-stu-id="90201-166">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://<sub domain>.filesanywhere.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="90201-167">Należy pamiętać, że nie są one hello wartości rzeczywistych.</span><span class="sxs-lookup"><span data-stu-id="90201-167">Please note that these are not hello real values.</span></span> <span data-ttu-id="90201-168">Masz tooupdate tych wartości za pomocą hello rzeczywiste na adres URL logowania i odpowiedzi adresu URL.</span><span class="sxs-lookup"><span data-stu-id="90201-168">You have tooupdate these values with hello actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="90201-169">Skontaktuj się z [zespołem pomocy technicznej FilesAnywhere](mailto:support@FilesAnywhere.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="90201-169">Contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) tooget these values.</span></span> 

5. <span data-ttu-id="90201-170">Aplikacja FilesAnywhere oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="90201-170">FilesAnywhere Software application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="90201-171">Skonfiguruj powitania po oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="90201-171">Please configure hello following claims for this application.</span></span> <span data-ttu-id="90201-172">Można zarządzać hello wartości tych atrybutów z hello "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="90201-172">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="90201-173">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="90201-173">hello following screenshot shows an example for this.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_filesanywhere_attribute.png)
    
    <span data-ttu-id="90201-175">Gdy hello znaki użytkowników zapasowej FilesAnywhere otrzymują wartość hello **clientid** atrybutu z [zespołu FilesAnywhere](mailto:support@FilesAnywhere.com).</span><span class="sxs-lookup"><span data-stu-id="90201-175">When hello users signs up with FilesAnywhere they get hello value of **clientid** attribute from [FilesAnywhere team](mailto:support@FilesAnywhere.com).</span></span> <span data-ttu-id="90201-176">Masz atrybutu "Identyfikator klienta" hello tooadd z unikatową wartość hello dostarczonych przez FilesAnywhere.</span><span class="sxs-lookup"><span data-stu-id="90201-176">You have tooadd hello "Client Id" attribute with hello unique value provided by FilesAnywhere.</span></span> <span data-ttu-id="90201-177">Te atrybuty pokazanym powyżej są wymagane.</span><span class="sxs-lookup"><span data-stu-id="90201-177">All these attributes shown above are required.</span></span>
    > [!NOTE] 
    > <span data-ttu-id="90201-178">Należy pamiętać, ta wartość hello **2331** z **clientid** jest tylko przykładowe.</span><span class="sxs-lookup"><span data-stu-id="90201-178">Please note that hello value **2331** of **clientid** is just an example.</span></span> <span data-ttu-id="90201-179">Należy tooprovide hello rzeczywistej wartości.</span><span class="sxs-lookup"><span data-stu-id="90201-179">You need tooprovide hello actual value.</span></span>


6. <span data-ttu-id="90201-180">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w powyższy obraz powitania i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="90201-180">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="90201-181">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="90201-181">Attribute Name</span></span> | <span data-ttu-id="90201-182">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="90201-182">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="90201-183">ClientID</span><span class="sxs-lookup"><span data-stu-id="90201-183">clientid</span></span> | <span data-ttu-id="90201-184">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="90201-184">*"uniquevalue"*</span></span> |

    <span data-ttu-id="90201-185">a.</span><span class="sxs-lookup"><span data-stu-id="90201-185">a.</span></span> <span data-ttu-id="90201-186">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="90201-186">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_05.png)
    
    <span data-ttu-id="90201-189">b.</span><span class="sxs-lookup"><span data-stu-id="90201-189">b.</span></span> <span data-ttu-id="90201-190">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="90201-190">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="90201-191">c.</span><span class="sxs-lookup"><span data-stu-id="90201-191">c.</span></span> <span data-ttu-id="90201-192">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="90201-192">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="90201-193">d.</span><span class="sxs-lookup"><span data-stu-id="90201-193">d.</span></span> <span data-ttu-id="90201-194">Kliknij przycisk **Ok**</span><span class="sxs-lookup"><span data-stu-id="90201-194">Click **Ok**</span></span>

7. <span data-ttu-id="90201-195">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="90201-195">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="90201-197">Na powitania **certyfikat podpisywania SAML** kliknij **certyfikatu (Base64)** , a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="90201-197">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_certificate.png) 

9. <span data-ttu-id="90201-199">Na powitania **konfiguracji FilesAnywhere** kliknij **skonfigurować FilesAnywhere** tooopen **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="90201-199">On hello **FilesAnywhere Configuration** section, click **Configure FilesAnywhere** tooopen **Configure sign-on** window.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configure.png) 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_configuresignon.png)

10. <span data-ttu-id="90201-202">Kończenie aplikacji na końcu FilesAnywhere, skontaktuj się z konfiguracji logowania jednokrotnego tooget [zespołem pomocy technicznej FilesAnywhere](mailto:support@FilesAnywhere.com) i podaj tokenu SAML hello pobrane podpisywania certyfikatu i jednego znaku w rejestracji jednokrotnej (SSO) adres URL.</span><span class="sxs-lookup"><span data-stu-id="90201-202">tooget SSO configuration complete for your application at FilesAnywhere end, contact [FilesAnywhere support team](mailto:support@FilesAnywhere.com) and provide them hello downloaded SAML token signing Certificate and Single Sign On (SSO) URL.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="90201-203">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="90201-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="90201-204">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu zarządzania Azure hello o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="90201-204">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="90201-206">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="90201-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="90201-207">W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="90201-207">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="90201-209">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="90201-209">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="90201-211">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="90201-211">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="90201-213">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="90201-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-FilesAnywhere-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="90201-215">a.</span><span class="sxs-lookup"><span data-stu-id="90201-215">a.</span></span> <span data-ttu-id="90201-216">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="90201-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="90201-217">b.</span><span class="sxs-lookup"><span data-stu-id="90201-217">b.</span></span> <span data-ttu-id="90201-218">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="90201-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="90201-219">c.</span><span class="sxs-lookup"><span data-stu-id="90201-219">c.</span></span> <span data-ttu-id="90201-220">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="90201-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="90201-221">d.</span><span class="sxs-lookup"><span data-stu-id="90201-221">d.</span></span> <span data-ttu-id="90201-222">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="90201-222">Click **Create**.</span></span> 



### <a name="creating-a-filesanywhere-test-user"></a><span data-ttu-id="90201-223">Tworzenie użytkownika testowego FilesAnywhere</span><span class="sxs-lookup"><span data-stu-id="90201-223">Creating a FilesAnywhere test user</span></span>

<span data-ttu-id="90201-224">Aplikacja obsługuje tylko w czasie Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników zostaną utworzone w aplikacji hello automatycznie.</span><span class="sxs-lookup"><span data-stu-id="90201-224">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> 


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="90201-225">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="90201-225">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="90201-226">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooFilesAnywhere dostępu.</span><span class="sxs-lookup"><span data-stu-id="90201-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooFilesAnywhere.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="90201-228">**tooassign tooFilesAnywhere Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="90201-228">**tooassign Britta Simon tooFilesAnywhere, perform hello following steps:**</span></span>

1. <span data-ttu-id="90201-229">W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="90201-229">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="90201-231">Z listy aplikacji hello wybierz **FilesAnywhere**.</span><span class="sxs-lookup"><span data-stu-id="90201-231">In hello applications list, select **FilesAnywhere**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_FilesAnywhere_app.png) 

3. <span data-ttu-id="90201-233">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="90201-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="90201-235">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="90201-235">Click **Add** button.</span></span> <span data-ttu-id="90201-236">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="90201-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="90201-238">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="90201-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="90201-239">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="90201-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="90201-240">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="90201-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="90201-241">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="90201-241">Testing single sign-on</span></span>

<span data-ttu-id="90201-242">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="90201-242">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="90201-243">Po kliknięciu kafelka FilesAnywhere hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour FilesAnywhere aplikacji.</span><span class="sxs-lookup"><span data-stu-id="90201-243">When you click hello FilesAnywhere tile in hello Access Panel, you should get automatically signed-on tooyour FilesAnywhere application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="90201-244">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="90201-244">Additional resources</span></span>

* [<span data-ttu-id="90201-245">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="90201-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="90201-246">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="90201-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-FilesAnywhere-tutorial/tutorial_general_203.png
