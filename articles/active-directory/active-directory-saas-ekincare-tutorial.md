---
title: 'Samouczek: Integracji Azure Active Directory z eKincare | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i eKincare."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 57f56d14-83cf-4cbb-b342-fac4fc60078f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 16129e3384132bb34744aadf088bb65f07ed7a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ekincare"></a><span data-ttu-id="e9872-103">Samouczek: Integracji Azure Active Directory z eKincare</span><span class="sxs-lookup"><span data-stu-id="e9872-103">Tutorial: Azure Active Directory integration with eKincare</span></span>

<span data-ttu-id="e9872-104">Z tego samouczka, dowiesz się, jak eKincare toointegrate w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e9872-104">In this tutorial, you learn how toointegrate eKincare with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e9872-105">Integracja z usługą Azure AD eKincare zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="e9872-105">Integrating eKincare with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e9872-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooeKincare</span><span class="sxs-lookup"><span data-stu-id="e9872-106">You can control in Azure AD who has access tooeKincare</span></span>
- <span data-ttu-id="e9872-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooeKincare (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9872-107">You can enable your users tooautomatically get signed-on tooeKincare (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e9872-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="e9872-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e9872-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e9872-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9872-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="e9872-110">Prerequisites</span></span>

<span data-ttu-id="e9872-111">tooconfigure integracji z usługą Azure AD z eKincare należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="e9872-111">tooconfigure Azure AD integration with eKincare, you need hello following items:</span></span>

- <span data-ttu-id="e9872-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9872-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e9872-113">EKincare jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="e9872-113">A eKincare single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e9872-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="e9872-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e9872-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="e9872-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e9872-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="e9872-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e9872-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e9872-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e9872-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="e9872-118">Scenario description</span></span>
<span data-ttu-id="e9872-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="e9872-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e9872-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="e9872-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e9872-121">Dodawanie eKincare z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e9872-121">Adding eKincare from hello gallery</span></span>
2. <span data-ttu-id="e9872-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e9872-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ekincare-from-hello-gallery"></a><span data-ttu-id="e9872-123">Dodawanie eKincare z galerii hello</span><span class="sxs-lookup"><span data-stu-id="e9872-123">Adding eKincare from hello gallery</span></span>
<span data-ttu-id="e9872-124">tooconfigure hello integracji eKincare do usługi Azure AD, należy eKincare tooadd z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="e9872-124">tooconfigure hello integration of eKincare into Azure AD, you need tooadd eKincare from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e9872-125">**eKincare tooadd z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e9872-125">**tooadd eKincare from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9872-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e9872-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="e9872-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="e9872-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e9872-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e9872-129">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="e9872-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e9872-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="e9872-133">W polu wyszukiwania hello wpisz **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="e9872-133">In hello search box, type **eKincare**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_search.png)

5. <span data-ttu-id="e9872-135">W panelu wyników hello zaznacz **eKincare**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="e9872-135">In hello results panel, select **eKincare**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e9872-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="e9872-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e9872-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z eKincare na podstawie użytkownika testowego, nazywany "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="e9872-138">In this section, you configure and test Azure AD single sign-on with eKincare based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e9872-139">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w eKincare jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9872-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in eKincare is tooa user in Azure AD.</span></span> <span data-ttu-id="e9872-140">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w eKincare musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="e9872-140">In other words, a link relationship between an Azure AD user and hello related user in eKincare needs toobe established.</span></span>

<span data-ttu-id="e9872-141">W eKincare, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="e9872-141">In eKincare, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="e9872-142">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z eKincare, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="e9872-142">tooconfigure and test Azure AD single sign-on with eKincare, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e9872-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="e9872-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e9872-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="e9872-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e9872-145">**[Tworzenie użytkownika testowego eKincare](#creating-a-ekincare-test-user)**  -toohave odpowiednikiem Simona Britta w eKincare, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e9872-145">**[Creating a eKincare test user](#creating-a-ekincare-test-user)** - toohave a counterpart of Britta Simon in eKincare that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e9872-146">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e9872-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e9872-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="e9872-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e9872-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e9872-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e9872-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure hello i skonfigurować logowanie jednokrotne w aplikacji eKincare.</span><span class="sxs-lookup"><span data-stu-id="e9872-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your eKincare application.</span></span>

<span data-ttu-id="e9872-150">**tooconfigure usługi Azure AD rejestracji jednokrotnej z eKincare, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e9872-150">**tooconfigure Azure AD single sign-on with eKincare, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9872-151">W portalu Azure na powitania hello **eKincare** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="e9872-151">In hello Azure portal, on hello **eKincare** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="e9872-153">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="e9872-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_samlbase.png)

3. <span data-ttu-id="e9872-155">Na powitania **eKincare domeny i adres URL** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="e9872-155">On hello **eKincare Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_url.png)

    <span data-ttu-id="e9872-157">a.</span><span class="sxs-lookup"><span data-stu-id="e9872-157">a.</span></span> <span data-ttu-id="e9872-158">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<instancename>.ekincare.com/`</span><span class="sxs-lookup"><span data-stu-id="e9872-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<instancename>.ekincare.com/`</span></span>

    <span data-ttu-id="e9872-159">b.</span><span class="sxs-lookup"><span data-stu-id="e9872-159">b.</span></span> <span data-ttu-id="e9872-160">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<instancename>.ekincare.com/hul/saml`</span><span class="sxs-lookup"><span data-stu-id="e9872-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<instancename>.ekincare.com/hul/saml`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e9872-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="e9872-161">These values are not real.</span></span> <span data-ttu-id="e9872-162">Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="e9872-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="e9872-163">Skontaktuj się z [zespołem pomocy technicznej eKincare](mailto:tech@ekincare.com) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="e9872-163">Contact [eKincare support team](mailto:tech@ekincare.com) tooget these values.</span></span>
 
4. <span data-ttu-id="e9872-164">Aplikacja eKincare oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="e9872-164">eKincare application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="e9872-165">Skonfiguruj powitania po oświadczeń dla tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e9872-165">Configure hello following claims for this application.</span></span> <span data-ttu-id="e9872-166">Można zarządzać hello wartości tych atrybutów z hello "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e9872-166">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="e9872-167">powitania po zrzut ekranu przedstawia przykład dla tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="e9872-167">hello following screenshot shows an example for this configuration.</span></span>

    <span data-ttu-id="e9872-168">Witaj Nazwa oświadczenia będzie zawsze **"identyfikator pracownika"** i wartość hello którego możemy zamapowaniu toouser.extensionattribute1, która zawiera identyfikator pracownika hello hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="e9872-168">hello claim name will always be **"employeeid"** and hello value of which we have mapped toouser.extensionattribute1, that contains hello employeeid of hello user.</span></span> <span data-ttu-id="e9872-169">Witaj tj nazwy innych dwa oświadczenia</span><span class="sxs-lookup"><span data-stu-id="e9872-169">hello other two claims' name i.e</span></span> <span data-ttu-id="e9872-170">**"identyfikatora organizacji"** i **"nazwa_organizacji"** jest zawsze tej samej i ich wartości zawierają szczegóły hello hello organizacji użytkownika hello odpowiednio.</span><span class="sxs-lookup"><span data-stu-id="e9872-170">**"organizationid"** and **"organizationname"** will always be same and their values contain hello details of hello organization of hello user respectively.</span></span>
    
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ekincare-tutorial/attribute.png)
    
5. <span data-ttu-id="e9872-172">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, skonfiguruj atrybut tokenu SAML, jak pokazano w powyższy obraz powitania i wykonywać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e9872-172">In hello **User Attributes** section on hello **Single sign-on** dialog, configure SAML token attribute as shown in hello image above and perform hello following steps:</span></span>
    
    | <span data-ttu-id="e9872-173">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="e9872-173">Attribute Name</span></span> | <span data-ttu-id="e9872-174">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="e9872-174">Attribute Value</span></span> |
    | ---------------| --------------- |    
    | <span data-ttu-id="e9872-175">Identyfikator pracownika</span><span class="sxs-lookup"><span data-stu-id="e9872-175">employeeid</span></span> | <span data-ttu-id="e9872-176">*User.extensionattribute1*</span><span class="sxs-lookup"><span data-stu-id="e9872-176">*user.extensionattribute1*</span></span> |
    | <span data-ttu-id="e9872-177">identyfikatora organizacji</span><span class="sxs-lookup"><span data-stu-id="e9872-177">organizationid</span></span> | <span data-ttu-id="e9872-178">*"uniquevalue"*</span><span class="sxs-lookup"><span data-stu-id="e9872-178">*"uniquevalue"*</span></span> |
    | <span data-ttu-id="e9872-179">nazwa_organizacji</span><span class="sxs-lookup"><span data-stu-id="e9872-179">organizationname</span></span> | <span data-ttu-id="e9872-180">*User.CompanyName*</span><span class="sxs-lookup"><span data-stu-id="e9872-180">*user.companyname*</span></span> |

    <span data-ttu-id="e9872-181">a.</span><span class="sxs-lookup"><span data-stu-id="e9872-181">a.</span></span> <span data-ttu-id="e9872-182">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e9872-182">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ekincare-tutorial/04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ekincare-tutorial/05.png)
    
    <span data-ttu-id="e9872-185">b.</span><span class="sxs-lookup"><span data-stu-id="e9872-185">b.</span></span> <span data-ttu-id="e9872-186">W hello **nazwa** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="e9872-186">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="e9872-187">c.</span><span class="sxs-lookup"><span data-stu-id="e9872-187">c.</span></span> <span data-ttu-id="e9872-188">Z hello **wartość** listy wartości atrybutu hello typ wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="e9872-188">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="e9872-189">d.</span><span class="sxs-lookup"><span data-stu-id="e9872-189">d.</span></span> <span data-ttu-id="e9872-190">Kliknij przycisk **Ok**</span><span class="sxs-lookup"><span data-stu-id="e9872-190">Click **Ok**</span></span>

6. <span data-ttu-id="e9872-191">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="e9872-191">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_certificate.png) 

7. <span data-ttu-id="e9872-193">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e9872-193">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ekincare-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="e9872-195">tooconfigure rejestracji jednokrotnej w **eKincare** strony, należy pobrać hello toosend **XML metadanych** za[zespołem pomocy technicznej eKincare](mailto:tech@ekincare.com).</span><span class="sxs-lookup"><span data-stu-id="e9872-195">tooconfigure single sign-on on **eKincare** side, you need toosend hello downloaded **Metadata XML** too[eKincare support team](mailto:tech@ekincare.com).</span></span> <span data-ttu-id="e9872-196">To ustawienie toohave hello prawidłowo po obu stronach połączenia logowania jednokrotnego SAML one ustawić.</span><span class="sxs-lookup"><span data-stu-id="e9872-196">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="e9872-197">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="e9872-197">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e9872-198">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="e9872-198">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e9872-199">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e9872-199">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e9872-200">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9872-200">Creating an Azure AD test user</span></span>
<span data-ttu-id="e9872-201">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="e9872-201">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="e9872-203">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="e9872-203">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9872-204">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="e9872-204">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e9872-206">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="e9872-206">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e9872-208">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e9872-208">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e9872-210">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="e9872-210">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-ekincare-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e9872-212">a.</span><span class="sxs-lookup"><span data-stu-id="e9872-212">a.</span></span> <span data-ttu-id="e9872-213">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e9872-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e9872-214">b.</span><span class="sxs-lookup"><span data-stu-id="e9872-214">b.</span></span> <span data-ttu-id="e9872-215">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e9872-215">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e9872-216">c.</span><span class="sxs-lookup"><span data-stu-id="e9872-216">c.</span></span> <span data-ttu-id="e9872-217">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="e9872-217">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e9872-218">d.</span><span class="sxs-lookup"><span data-stu-id="e9872-218">d.</span></span> <span data-ttu-id="e9872-219">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="e9872-219">Click **Create**.</span></span>
 
### <a name="creating-a-ekincare-test-user"></a><span data-ttu-id="e9872-220">Tworzenie użytkownika testowego eKincare</span><span class="sxs-lookup"><span data-stu-id="e9872-220">Creating a eKincare test user</span></span>

<span data-ttu-id="e9872-221">Aplikacja obsługuje tylko w czasie Inicjowanie obsługi użytkowników i uwierzytelnianie użytkowników są tworzone automatycznie w aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e9872-221">Application supports Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e9872-222">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e9872-222">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e9872-223">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooeKincare.</span><span class="sxs-lookup"><span data-stu-id="e9872-223">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooeKincare.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="e9872-225">**tooassign tooeKincare Simona Britta wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="e9872-225">**tooassign Britta Simon tooeKincare, perform hello following steps:**</span></span>

1. <span data-ttu-id="e9872-226">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="e9872-226">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="e9872-228">Z listy aplikacji hello wybierz **eKincare**.</span><span class="sxs-lookup"><span data-stu-id="e9872-228">In hello applications list, select **eKincare**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-ekincare-tutorial/tutorial_ekincare_app.png) 

3. <span data-ttu-id="e9872-230">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="e9872-230">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="e9872-232">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="e9872-232">Click **Add** button.</span></span> <span data-ttu-id="e9872-233">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e9872-233">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="e9872-235">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="e9872-235">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e9872-236">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e9872-236">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e9872-237">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="e9872-237">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e9872-238">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="e9872-238">Testing single sign-on</span></span>

<span data-ttu-id="e9872-239">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="e9872-239">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e9872-240">Po kliknięciu kafelka eKincare hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour eKincare aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e9872-240">When you click hello eKincare tile in hello Access Panel, you should get automatically signed-on tooyour eKincare application.</span></span>
<span data-ttu-id="e9872-241">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="e9872-241">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md)</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e9872-242">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="e9872-242">Additional resources</span></span>

* [<span data-ttu-id="e9872-243">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e9872-243">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e9872-244">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e9872-244">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ekincare-tutorial/tutorial_general_203.png

