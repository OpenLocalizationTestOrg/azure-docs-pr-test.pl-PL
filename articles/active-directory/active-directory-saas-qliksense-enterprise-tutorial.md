---
title: "Samouczek: Integracji Azure Active Directory z przedsiębiorstwa znaczeniu Qlik | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i Qlik przedsiębiorstwa znaczeniu."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 8c27e340-2b25-47b6-bf1f-438be4c14f93
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 153edb3f8cd41790d4e9a74f15cfb806e5e9e3b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qlik-sense-enterprise"></a><span data-ttu-id="6c537-103">Samouczek: Integracji Azure Active Directory z przedsiębiorstwa znaczeniu Qlik</span><span class="sxs-lookup"><span data-stu-id="6c537-103">Tutorial: Azure Active Directory integration with Qlik Sense Enterprise</span></span>

<span data-ttu-id="6c537-104">Z tego samouczka, dowiesz się, jak toointegrate Qlik znaczeniu przedsiębiorstwa w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6c537-104">In this tutorial, you learn how toointegrate Qlik Sense Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6c537-105">Integracja z usługą Azure AD przedsiębiorstwa znaczeniu Qlik zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="6c537-105">Integrating Qlik Sense Enterprise with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="6c537-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooQlik przedsiębiorstwa znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="6c537-106">You can control in Azure AD who has access tooQlik Sense Enterprise.</span></span>
- <span data-ttu-id="6c537-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooQlik przedsiębiorstwa znaczeniu (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c537-107">You can enable your users tooautomatically get signed-on tooQlik Sense Enterprise (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="6c537-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6c537-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="6c537-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6c537-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6c537-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="6c537-110">Prerequisites</span></span>

<span data-ttu-id="6c537-111">tooconfigure integracji usługi Azure AD z Qlik przedsiębiorstwa znaczeniu, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="6c537-111">tooconfigure Azure AD integration with Qlik Sense Enterprise, you need hello following items:</span></span>

- <span data-ttu-id="6c537-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c537-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6c537-113">Przedsiębiorstwa znaczeniu Qlik logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="6c537-113">A Qlik Sense Enterprise single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6c537-114">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="6c537-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6c537-115">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="6c537-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6c537-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="6c537-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6c537-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6c537-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6c537-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="6c537-118">Scenario description</span></span>
<span data-ttu-id="6c537-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="6c537-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6c537-120">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="6c537-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6c537-121">Dodawanie przedsiębiorstwa znaczeniu Qlik z galerii hello</span><span class="sxs-lookup"><span data-stu-id="6c537-121">Adding Qlik Sense Enterprise from hello gallery</span></span>
2. <span data-ttu-id="6c537-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="6c537-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-qlik-sense-enterprise-from-hello-gallery"></a><span data-ttu-id="6c537-123">Dodawanie przedsiębiorstwa znaczeniu Qlik z galerii hello</span><span class="sxs-lookup"><span data-stu-id="6c537-123">Adding Qlik Sense Enterprise from hello gallery</span></span>
<span data-ttu-id="6c537-124">tooconfigure hello integracji przedsiębiorstwa znaczeniu Qlik do usługi Azure AD, należy tooadd przedsiębiorstwa znaczeniu Qlik z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="6c537-124">tooconfigure hello integration of Qlik Sense Enterprise into Azure AD, you need tooadd Qlik Sense Enterprise from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="6c537-125">**tooadd przedsiębiorstwa znaczeniu Qlik z galerii hello wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="6c537-125">**tooadd Qlik Sense Enterprise from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="6c537-126">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="6c537-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="6c537-128">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="6c537-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="6c537-129">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6c537-129">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="6c537-131">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6c537-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="6c537-133">W polu wyszukiwania hello wpisz **przedsiębiorstwa znaczeniu Qlik**, wybierz pozycję **przedsiębiorstwa znaczeniu Qlik** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="6c537-133">In hello search box, type **Qlik Sense Enterprise**, select **Qlik Sense Enterprise** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Przedsiębiorstwa znaczeniu Qlik hello listy wyników](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="6c537-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6c537-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="6c537-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Qlik przedsiębiorstwa znaczeniu, w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="6c537-136">In this section, you configure and test Azure AD single sign-on with Qlik Sense Enterprise based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="6c537-137">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w przedsiębiorstwie znaczeniu Qlik jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c537-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Qlik Sense Enterprise is tooa user in Azure AD.</span></span> <span data-ttu-id="6c537-138">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w przedsiębiorstwie znaczeniu Qlik musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="6c537-138">In other words, a link relationship between an Azure AD user and hello related user in Qlik Sense Enterprise needs toobe established.</span></span>

<span data-ttu-id="6c537-139">W Qlik przedsiębiorstwa znaczeniu, należy przypisać wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="6c537-139">In Qlik Sense Enterprise, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="6c537-140">tooconfigure i testowych usługi Azure AD rejestracji jednokrotnej z Qlik przedsiębiorstwa znaczeniu, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="6c537-140">tooconfigure and test Azure AD single sign-on with Qlik Sense Enterprise, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="6c537-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="6c537-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="6c537-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6c537-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6c537-143">**[Tworzenie użytkownika testowego przedsiębiorstwa znaczeniu Qlik](#create-a-qlik-sense-enterprise-test-user)**  -toohave odpowiednikiem Simona Britta w przedsiębiorstwie znaczeniu Qlik, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="6c537-143">**[Create a Qlik Sense Enterprise test user](#create-a-qlik-sense-enterprise-test-user)** - toohave a counterpart of Britta Simon in Qlik Sense Enterprise that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="6c537-144">**[Przypisz użytkownika testowego hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6c537-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6c537-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="6c537-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="6c537-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6c537-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="6c537-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji przedsiębiorstwa znaczeniu Qlik.</span><span class="sxs-lookup"><span data-stu-id="6c537-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Qlik Sense Enterprise application.</span></span>

<span data-ttu-id="6c537-148">**tooconfigure usługi Azure AD rejestracji jednokrotnej z Qlik przedsiębiorstwa znaczeniu, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="6c537-148">**tooconfigure Azure AD single sign-on with Qlik Sense Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="6c537-149">W portalu Azure na powitania hello **przedsiębiorstwa znaczeniu Qlik** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="6c537-149">In hello Azure portal, on hello **Qlik Sense Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="6c537-151">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6c537-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_samlbase.png)

3. <span data-ttu-id="6c537-153">Na powitania **adresy URL i domeny przedsiębiorstwa znaczeniu Qlik** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="6c537-153">On hello **Qlik Sense Enterprise Domain and URLs** section, perform hello following steps:</span></span>

    ![Adresy URL i domeny przedsiębiorstwa znaczeniu Qlik pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_url.png)

    <span data-ttu-id="6c537-155">a.</span><span class="sxs-lookup"><span data-stu-id="6c537-155">a.</span></span> <span data-ttu-id="6c537-156">W hello **adres URL logowania** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span><span class="sxs-lookup"><span data-stu-id="6c537-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<Qlik Sense Fully Qualifed Hostname>:443//samlauthn/`</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="6c537-157">Należy zwrócić uwagę hello kończyć się ukośnikiem na końcu hello tego identyfikatora URI.</span><span class="sxs-lookup"><span data-stu-id="6c537-157">Note hello trailing slash at hello end of this URI.</span></span> <span data-ttu-id="6c537-158">Jest wymagane.</span><span class="sxs-lookup"><span data-stu-id="6c537-158">It is required.</span></span>
    
    <span data-ttu-id="6c537-159">b.</span><span class="sxs-lookup"><span data-stu-id="6c537-159">b.</span></span> <span data-ttu-id="6c537-160">W hello **identyfikator** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:</span><span class="sxs-lookup"><span data-stu-id="6c537-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qlikpoc.com`|
    | `https://<Qlik Sense Fully Qualifed Hostname>.qliksense.com`|

    > [!NOTE] 
    > <span data-ttu-id="6c537-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="6c537-161">These values are not real.</span></span> <span data-ttu-id="6c537-162">Aktualizacja tych wartości za pomocą hello rzeczywisty adres URL logowania i identyfikator, które opisano szczegółowo w dalszej części tego samouczka lub skontaktuj się z [zespołem pomocy technicznej klienta przedsiębiorstwa znaczeniu Qlik](https://www.qlik.com/us/services/support) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="6c537-162">Update these values with hello actual Sign-On URL and Identifier, Which are explained later in this tutorial or contact [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) tooget these values.</span></span> 

4. <span data-ttu-id="6c537-163">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="6c537-163">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_certificate.png) 

5. <span data-ttu-id="6c537-165">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6c537-165">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6c537-167">Przygotuj plik XML metadanych Federacji hello, dzięki czemu możesz przekazać ten serwer znaczeniu tooQlik.</span><span class="sxs-lookup"><span data-stu-id="6c537-167">Prepare hello Federation Metadata XML file so that you can upload that tooQlik Sense server.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="6c537-168">Przed przekazaniem hello IdP metadanych toohello serwera Qlik znaczeniu, plik hello musi toobe edytować tooremove informacji tooensure poprawne działanie między usługą Azure AD i serwer Qlik znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="6c537-168">Before uploading hello IdP metadata toohello Qlik Sense server, hello file needs toobe edited tooremove information tooensure proper operation between Azure AD and Qlik Sense server.</span></span>
    
    ![QlikSense][qs24]
   
    <span data-ttu-id="6c537-170">a.</span><span class="sxs-lookup"><span data-stu-id="6c537-170">a.</span></span> <span data-ttu-id="6c537-171">Otwórz plik FederationMetaData.xml hello, który został pobrany z portalu Azure w edytorze tekstów.</span><span class="sxs-lookup"><span data-stu-id="6c537-171">Open hello FederationMetaData.xml file, which you have downloaded from Azure portal in a text editor.</span></span>
   
    <span data-ttu-id="6c537-172">b.</span><span class="sxs-lookup"><span data-stu-id="6c537-172">b.</span></span> <span data-ttu-id="6c537-173">Wyszukaj wartości hello **RoleDescriptor**.</span><span class="sxs-lookup"><span data-stu-id="6c537-173">Search for hello value **RoleDescriptor**.</span></span>  <span data-ttu-id="6c537-174">Istnieją cztery wpisy (dwie pary otwierające i zamykające znaczniki elementów).</span><span class="sxs-lookup"><span data-stu-id="6c537-174">There are four entries (two pairs of opening and closing element tags).</span></span>
   
    <span data-ttu-id="6c537-175">c.</span><span class="sxs-lookup"><span data-stu-id="6c537-175">c.</span></span> <span data-ttu-id="6c537-176">Usuwania hello RoleDescriptor tagów i wszystkie informacje między hello pliku.</span><span class="sxs-lookup"><span data-stu-id="6c537-176">Delete hello RoleDescriptor tags and all information in between from hello file.</span></span>
   
    <span data-ttu-id="6c537-177">d.</span><span class="sxs-lookup"><span data-stu-id="6c537-177">d.</span></span> <span data-ttu-id="6c537-178">Zapisz plik hello i przechowywać w pobliżu do użytku w dalszej części tego dokumentu.</span><span class="sxs-lookup"><span data-stu-id="6c537-178">Save hello file and keep it nearby for use later in this document.</span></span>

7. <span data-ttu-id="6c537-179">Przejdź toohello Qlik znaczeniu Qlik Management Console (QMC) jako użytkownik, który można utworzyć konfiguracji wirtualnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="6c537-179">Navigate toohello Qlik Sense Qlik Management Console (QMC) as a user who can create virtual proxy configurations.</span></span>

8. <span data-ttu-id="6c537-180">Witaj QMC polecenie hello **wirtualnych serwerów proxy** elementu menu.</span><span class="sxs-lookup"><span data-stu-id="6c537-180">In hello QMC, click on hello **Virtual Proxies** menu item.</span></span>
   
    ![QlikSense][qs6] 

9. <span data-ttu-id="6c537-182">U dołu hello hello ekranu, kliknij przycisk hello **Utwórz nowy** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6c537-182">At hello bottom of hello screen, click hello **Create new** button.</span></span>
   
    ![QlikSense][qs7]

10. <span data-ttu-id="6c537-184">zostanie wyświetlony ekran edycji proxy wirtualnej Hello.</span><span class="sxs-lookup"><span data-stu-id="6c537-184">hello Virtual proxy edit screen appears.</span></span>  <span data-ttu-id="6c537-185">Na powitania prawej krawędzi ekranu hello jest menu do wybierania opcji konfiguracji widoczne.</span><span class="sxs-lookup"><span data-stu-id="6c537-185">On hello right side of hello screen is a menu for making configuration options visible.</span></span>
   
    ![QlikSense][qs9]

11. <span data-ttu-id="6c537-187">Z zaznaczoną opcją menu identyfikacji hello wprowadź informacje identyfikujące hello hello konfiguracji serwera proxy wirtualnych Azure.</span><span class="sxs-lookup"><span data-stu-id="6c537-187">With hello Identification menu option checked, enter hello identifying information for hello Azure virtual proxy configuration.</span></span>
    
    ![QlikSense][qs8]  
    
    <span data-ttu-id="6c537-189">a.</span><span class="sxs-lookup"><span data-stu-id="6c537-189">a.</span></span> <span data-ttu-id="6c537-190">Witaj **opis** pole jest przyjazną nazwę dla konfiguracji serwera proxy wirtualnego hello.</span><span class="sxs-lookup"><span data-stu-id="6c537-190">hello **Description** field is a friendly name for hello virtual proxy configuration.</span></span>  <span data-ttu-id="6c537-191">Wprowadź wartość opis.</span><span class="sxs-lookup"><span data-stu-id="6c537-191">Enter a value for a description.</span></span>
    
    <span data-ttu-id="6c537-192">b.</span><span class="sxs-lookup"><span data-stu-id="6c537-192">b.</span></span> <span data-ttu-id="6c537-193">Witaj **prefiksu** pole identyfikuje punkt końcowy wirtualnego serwera proxy hello podłączania tooQlik znaczeniu z usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6c537-193">hello **Prefix** field identifies hello virtual proxy endpoint for connecting tooQlik Sense with Azure AD Single Sign-On.</span></span>  <span data-ttu-id="6c537-194">Wprowadź nazwę unikatowy prefiks dla tego wirtualnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="6c537-194">Enter a unique prefix name for this virtual proxy.</span></span>
    
    <span data-ttu-id="6c537-195">c.</span><span class="sxs-lookup"><span data-stu-id="6c537-195">c.</span></span> <span data-ttu-id="6c537-196">**Limit czasu bezczynności sesji (w minutach)** jest hello przekroczenia limitu czasu dla połączeń za pośrednictwem tego wirtualnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="6c537-196">**Session inactivity timeout (minutes)** is hello timeout for connections through this virtual proxy.</span></span>
    
    <span data-ttu-id="6c537-197">d.</span><span class="sxs-lookup"><span data-stu-id="6c537-197">d.</span></span> <span data-ttu-id="6c537-198">Witaj **nazwy nagłówka pliku cookie sesji** jest przechowywanie nazwę pliku cookie hello hello identyfikator sesji hello znaczeniu Qlik sesji przez użytkownika otrzymuje po pomyślnym uwierzytelnieniu.</span><span class="sxs-lookup"><span data-stu-id="6c537-198">hello **Session cookie header name** is hello cookie name storing hello session identifier for hello Qlik Sense session a user receives after successful authentication.</span></span>  <span data-ttu-id="6c537-199">Ta nazwa musi być unikatowa.</span><span class="sxs-lookup"><span data-stu-id="6c537-199">This name must be unique.</span></span>

12. <span data-ttu-id="6c537-200">Polecenie hello uwierzytelniania menu opcji toomake on widoczny.</span><span class="sxs-lookup"><span data-stu-id="6c537-200">Click on hello Authentication menu option toomake it visible.</span></span>  <span data-ttu-id="6c537-201">zostanie wyświetlony ekran uwierzytelniania Hello.</span><span class="sxs-lookup"><span data-stu-id="6c537-201">hello Authentication screen appears.</span></span>
    
    ![QlikSense][qs10]
    
    <span data-ttu-id="6c537-203">a.</span><span class="sxs-lookup"><span data-stu-id="6c537-203">a.</span></span> <span data-ttu-id="6c537-204">Hello **tryb dostępu anonimowego** listy rozwijanej określa użytkowników anonimowych może udostępniać znaczeniu Qlik za pośrednictwem hello wirtualnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="6c537-204">hello **Anonymous access mode** drop down determines if anonymous users may access Qlik Sense through hello virtual proxy.</span></span>  <span data-ttu-id="6c537-205">Opcja domyślna Hello jest nie użytkownika anonimowego.</span><span class="sxs-lookup"><span data-stu-id="6c537-205">hello default option is No anonymous user.</span></span>
    
    <span data-ttu-id="6c537-206">b.</span><span class="sxs-lookup"><span data-stu-id="6c537-206">b.</span></span> <span data-ttu-id="6c537-207">Witaj **metodę uwierzytelniania** listy rozwijanej określa użyje hello uwierzytelniania schemat hello wirtualnego proxy.</span><span class="sxs-lookup"><span data-stu-id="6c537-207">hello **Authentication method** drop-down determines hello authentication scheme hello virtual proxy will use.</span></span>  <span data-ttu-id="6c537-208">Z listy rozwijanej hello wybierz SAML.</span><span class="sxs-lookup"><span data-stu-id="6c537-208">Select SAML from hello drop-down list.</span></span>  <span data-ttu-id="6c537-209">W związku z tym pojawi się więcej opcji.</span><span class="sxs-lookup"><span data-stu-id="6c537-209">More options appear as a result.</span></span>
    
    <span data-ttu-id="6c537-210">c.</span><span class="sxs-lookup"><span data-stu-id="6c537-210">c.</span></span> <span data-ttu-id="6c537-211">W hello **pola identyfikatora URI hosta SAML**, wejściowych hello hostname wprowadzania tooaccess znaczeniu Qlik za pośrednictwem tego serwera proxy do wirtualnego SAML.</span><span class="sxs-lookup"><span data-stu-id="6c537-211">In hello **SAML host URI field**, input hello hostname users enter tooaccess Qlik Sense through this SAML virtual proxy.</span></span>  <span data-ttu-id="6c537-212">Nazwa hosta Hello jest identyfikator uri hello powitania serwera Qlik znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="6c537-212">hello hostname is hello uri of hello Qlik Sense server.</span></span>
    
    <span data-ttu-id="6c537-213">d.</span><span class="sxs-lookup"><span data-stu-id="6c537-213">d.</span></span> <span data-ttu-id="6c537-214">W hello **identyfikator jednostki SAML**, wprowadź hello tę samą wartość wprowadzona w polu identyfikatora URI hosta SAML hello.</span><span class="sxs-lookup"><span data-stu-id="6c537-214">In hello **SAML entity ID**, enter hello same value entered for hello SAML host URI field.</span></span>
    
    <span data-ttu-id="6c537-215">e.</span><span class="sxs-lookup"><span data-stu-id="6c537-215">e.</span></span> <span data-ttu-id="6c537-216">Hello **metadanych SAML IdP** jest plikiem hello edytować we wcześniejszej części hello **edytowanie metadanych federacji z konfiguracji usługi Azure AD** sekcji.</span><span class="sxs-lookup"><span data-stu-id="6c537-216">hello **SAML IdP metadata** is hello file edited earlier in hello **Edit Federation Metadata from Azure AD Configuration** section.</span></span>  <span data-ttu-id="6c537-217">**Przed przekazaniem hello IdP metadanych pliku hello musi toobe edytować** poprawne działanie tooensure tooremove informacji między usługą Azure AD i serwer Qlik znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="6c537-217">**Before uploading hello IdP metadata, hello file needs toobe edited** tooremove information tooensure proper operation between Azure AD and Qlik Sense server.</span></span>  <span data-ttu-id="6c537-218">**Jeśli plik hello ma jeszcze edytować toobe należy zapoznać się z powyższych instrukcji toohello.**</span><span class="sxs-lookup"><span data-stu-id="6c537-218">**Please refer toohello instructions above if hello file has yet toobe edited.**</span></span>  <span data-ttu-id="6c537-219">Jeśli edytowano hello pliku kliknij hello przycisk Przeglądaj i wybierz hello metadanych edytowanego pliku tooupload go toohello konfiguracji wirtualnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="6c537-219">If hello file has been edited click on hello Browse button and select hello edited metadata file tooupload it toohello virtual proxy configuration.</span></span>
    
    <span data-ttu-id="6c537-220">f.</span><span class="sxs-lookup"><span data-stu-id="6c537-220">f.</span></span> <span data-ttu-id="6c537-221">Wprowadź hello atrybut nazwy lub schematu odwołanie do atrybutu SAML hello reprezentujący hello **UserID** toohello znaczeniu Qlik serwer wysyła usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c537-221">Enter hello attribute name or schema reference for hello SAML attribute representing hello **UserID** Azure AD sends toohello Qlik Sense server.</span></span>  <span data-ttu-id="6c537-222">Informacje o odwołaniu schematu jest dostępna w konfiguracji wpisu ekrany Azure aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6c537-222">Schema reference information is available in hello Azure app screens post configuration.</span></span>  <span data-ttu-id="6c537-223">Atrybut nazwy hello toouse, wprowadź `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="6c537-223">toouse hello name attribute, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="6c537-224">g.</span><span class="sxs-lookup"><span data-stu-id="6c537-224">g.</span></span> <span data-ttu-id="6c537-225">Wprowadź wartość hello hello **katalogu użytkownika** który będzie dołączony toousers podczas uwierzytelniania serwera znaczeniu tooQlik za pośrednictwem usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c537-225">Enter hello value for hello **user directory** that will be attached toousers when they authenticate tooQlik Sense server through Azure AD.</span></span>  <span data-ttu-id="6c537-226">Wartości zapisane na stałe muszą być ujęte w **nawiasy kwadratowe []**.</span><span class="sxs-lookup"><span data-stu-id="6c537-226">Hardcoded values must be surrounded by **square brackets []**.</span></span>  <span data-ttu-id="6c537-227">toouse atrybut wysyłane w hello potwierdzenia języka SAML programu Azure AD, wprowadź nazwę hello atrybutu hello w tym polu tekstowym **bez** nawiasy kwadratowe.</span><span class="sxs-lookup"><span data-stu-id="6c537-227">toouse an attribute sent in hello Azure AD SAML assertion, enter hello name of hello attribute in this text box **without** square brackets.</span></span>
    
    <span data-ttu-id="6c537-228">h.</span><span class="sxs-lookup"><span data-stu-id="6c537-228">h.</span></span> <span data-ttu-id="6c537-229">Witaj **algorytm podpisywania SAML** zestawy hello usługi dostawcy (w tym wielkość server znaczeniu Qlik) certyfikatu podpisywania hello konfiguracji wirtualnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="6c537-229">hello **SAML signing algorithm** sets hello service provider (in this case Qlik Sense server) certificate signing for hello virtual proxy configuration.</span></span>  <span data-ttu-id="6c537-230">Jeśli serwer znaczeniu Qlik używa zaufanego certyfikatu wygenerowanych przy użyciu Microsoft Enhanced RSA and AES Cryptographic Provider, zmień algorytm podpisywania SAML hello zbyt**algorytmu SHA-256**.</span><span class="sxs-lookup"><span data-stu-id="6c537-230">If Qlik Sense server uses a trusted certificate generated using Microsoft Enhanced RSA and AES Cryptographic Provider, change hello SAML signing algorithm too**SHA-256**.</span></span>
    
    <span data-ttu-id="6c537-231">i.</span><span class="sxs-lookup"><span data-stu-id="6c537-231">i.</span></span> <span data-ttu-id="6c537-232">Witaj SAML atrybutu mapowania sekcji umożliwia dodatkowych atrybutów, takich jak grupy toobe wysyłane tooQlik znaczeniu do użycia w zasadach zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="6c537-232">hello SAML attribute mapping section allows for additional attributes like groups toobe sent tooQlik Sense for use in security rules.</span></span>

13. <span data-ttu-id="6c537-233">Polecenie hello **RÓWNOWAŻENIA obciążenia** toomake opcji menu on widoczny.</span><span class="sxs-lookup"><span data-stu-id="6c537-233">Click on hello **LOAD BALANCING** menu option toomake it visible.</span></span>  <span data-ttu-id="6c537-234">zostanie wyświetlony ekran równoważenia obciążenia Hello.</span><span class="sxs-lookup"><span data-stu-id="6c537-234">hello Load Balancing screen appears.</span></span>
    
    ![QlikSense][qs11]

14. <span data-ttu-id="6c537-236">Polecenie hello **Dodaj nowy węzeł serwera** przycisku wybierz aparat węzła lub węzłów znaczeniu Qlik wysyła celów równoważenia obciążenia toofor sesji i kliknij przycisk hello **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6c537-236">Click on hello **Add new server node** button, select engine node or nodes Qlik Sense will send sessions toofor load balancing purposes, and click hello **Add** button.</span></span>
    
    ![QlikSense][qs12]

15. <span data-ttu-id="6c537-238">Polecenie hello menu zaawansowanych opcji toomake on widoczny.</span><span class="sxs-lookup"><span data-stu-id="6c537-238">Click on hello Advanced menu option toomake it visible.</span></span> <span data-ttu-id="6c537-239">zostanie wyświetlony ekran Zaawansowane Hello.</span><span class="sxs-lookup"><span data-stu-id="6c537-239">hello Advanced screen appears.</span></span>
    
    ![QlikSense][qs13]
    
    <span data-ttu-id="6c537-241">Witaj hosta białą listę identyfikuje nazwy hostów, które są akceptowane, gdy połączenie toohello serwera Qlik znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="6c537-241">hello Host white list identifies hostnames that are accepted when connecting toohello Qlik Sense server.</span></span>  <span data-ttu-id="6c537-242">**Wprowadź nazwę hosta hello, którą użytkownicy określą podczas łączenia serwera znaczeniu tooQlik.**</span><span class="sxs-lookup"><span data-stu-id="6c537-242">**Enter hello hostname users will specify when connecting tooQlik Sense server.**</span></span> <span data-ttu-id="6c537-243">Nazwa hosta Hello jest hello samą wartość jak hello SAML identyfikatora uri hosta bez hello https://.</span><span class="sxs-lookup"><span data-stu-id="6c537-243">hello hostname is hello same value as hello SAML host uri without hello https://.</span></span>

16. <span data-ttu-id="6c537-244">Kliknij przycisk hello **Zastosuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6c537-244">Click hello **Apply** button.</span></span>
    
    ![QlikSense][qs14]

17. <span data-ttu-id="6c537-246">Kliknij przycisk OK tooaccept hello ostrzeżenie dotyczące serwerów proxy zostanie uruchomiona ponownie połączony toohello wirtualnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="6c537-246">Click OK tooaccept hello warning message that states proxies linked toohello virtual proxy will be restarted.</span></span>
    
    ![QlikSense][qs15]

18. <span data-ttu-id="6c537-248">Po prawej stronie powitania ekranie powitania pojawi się hello skojarzone elementy menu.</span><span class="sxs-lookup"><span data-stu-id="6c537-248">On hello right side of hello screen, hello Associated items menu appears.</span></span>  <span data-ttu-id="6c537-249">Polecenie hello **proxy** opcji menu.</span><span class="sxs-lookup"><span data-stu-id="6c537-249">Click on hello **Proxies** menu option.</span></span>
    
    ![QlikSense][qs16]

19. <span data-ttu-id="6c537-251">zostanie wyświetlony ekran proxy Hello.</span><span class="sxs-lookup"><span data-stu-id="6c537-251">hello proxy screen appears.</span></span>  <span data-ttu-id="6c537-252">Kliknij przycisk hello **łącze** znajdujący się u toolink dolnej hello proxy wirtualnego toohello serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="6c537-252">Click hello **Link** button at hello bottom toolink a proxy toohello virtual proxy.</span></span>
    
    ![QlikSense][qs17]

20. <span data-ttu-id="6c537-254">Wybierz hello węzeł serwera proxy, który obsługi tego połączenia wirtualnego serwera proxy i kliknij przycisk hello **łącze** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6c537-254">Select hello proxy node that will support this virtual proxy connection and click hello **Link** button.</span></span>  <span data-ttu-id="6c537-255">Po połączeniu, powitania serwera proxy, będą wyświetlane w skojarzone serwery proxy.</span><span class="sxs-lookup"><span data-stu-id="6c537-255">After linking, hello proxy will be listed under associated proxies.</span></span>
    
    ![QlikSense][qs18]
  
    ![QlikSense][qs19]

21. <span data-ttu-id="6c537-258">Po około pięciu sekundach tooten, Odśwież QMC wiadomość hello będą wyświetlane.</span><span class="sxs-lookup"><span data-stu-id="6c537-258">After about five tooten seconds, hello Refresh QMC message will appear.</span></span>  <span data-ttu-id="6c537-259">Kliknij przycisk hello **Odśwież QMC** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6c537-259">Click hello **Refresh QMC** button.</span></span>
    
    ![QlikSense][qs20]

22. <span data-ttu-id="6c537-261">Po odświeżeniu hello QMC na powitania kliknij przycisk **proxy wirtualnej** elementu menu.</span><span class="sxs-lookup"><span data-stu-id="6c537-261">When hello QMC refreshes, click on hello **Virtual proxies** menu item.</span></span> <span data-ttu-id="6c537-262">Nowy wpis wirtualnego serwera proxy SAML Hello to wymienione w tabeli hello na ekranie powitania.</span><span class="sxs-lookup"><span data-stu-id="6c537-262">hello new SAML virtual proxy entry is listed in hello table on hello screen.</span></span>  <span data-ttu-id="6c537-263">Kliknij wpis wirtualnego serwera proxy hello.</span><span class="sxs-lookup"><span data-stu-id="6c537-263">Single click on hello virtual proxy entry.</span></span>
    
    ![QlikSense][qs51]

23. <span data-ttu-id="6c537-265">U dołu hello hello ekranu hello SP pobrać metadanych przycisk zostanie aktywowany.</span><span class="sxs-lookup"><span data-stu-id="6c537-265">At hello bottom of hello screen, hello Download SP metadata button will activate.</span></span>  <span data-ttu-id="6c537-266">Kliknij przycisk hello **SP pobrać metadanych** pliku tooa przycisk toosave hello metadanych.</span><span class="sxs-lookup"><span data-stu-id="6c537-266">Click hello **Download SP metadata** button toosave hello metadata tooa file.</span></span>
    
    ![QlikSense][qs52]

24. <span data-ttu-id="6c537-268">Otwórz hello sp pliku metadanych.</span><span class="sxs-lookup"><span data-stu-id="6c537-268">Open hello sp metadata file.</span></span>  <span data-ttu-id="6c537-269">Obserwować hello **entityID** wpisu i hello **AssertionConsumerService** wpisu.</span><span class="sxs-lookup"><span data-stu-id="6c537-269">Observe hello **entityID** entry and hello **AssertionConsumerService** entry.</span></span>  <span data-ttu-id="6c537-270">Te wartości są równoważne toohello **identyfikator** i hello **Zaloguj się na adres URL** w konfiguracji aplikacji hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6c537-270">These values are equivalent toohello **Identifier** and hello **Sign on URL** in hello Azure AD application configuration.</span></span> <span data-ttu-id="6c537-271">Wklej te wartości w hello **adresy URL i domeny przedsiębiorstwa znaczeniu Qlik** sekcji w konfiguracji aplikacji hello Azure AD, jeśli ich są niezgodne, a następnie należy zastąpić je w Kreatorze konfiguracji usługi Azure AD aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="6c537-271">Paste these values in hello **Qlik Sense Enterprise Domain and URLs** section in hello Azure AD application configuration if they are not matching, then you should replace them in hello Azure AD App configuration wizard.</span></span>
    
    ![QlikSense][qs53]

> [!TIP]
> <span data-ttu-id="6c537-273">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="6c537-273">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="6c537-274">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="6c537-274">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="6c537-275">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="6c537-275">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="6c537-276">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c537-276">Create an Azure AD test user</span></span>
<span data-ttu-id="6c537-277">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="6c537-277">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="6c537-279">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="6c537-279">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="6c537-280">W portalu Azure, w okienku po lewej stronie powitania hello kliknij hello **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6c537-280">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

   ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="6c537-282">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="6c537-282">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

   ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="6c537-284">Witaj tooopen **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** u góry hello hello **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="6c537-284">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

   ![przycisk Dodaj Hello](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="6c537-286">W hello **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="6c537-286">In hello **User** dialog box, perform hello following steps:</span></span>

   ![okno dialogowe Hello użytkownika](./media/active-directory-saas-qliksense-enterprise-tutorial/create_aaduser_04.png)

   <span data-ttu-id="6c537-288">a.</span><span class="sxs-lookup"><span data-stu-id="6c537-288">a.</span></span> <span data-ttu-id="6c537-289">W hello **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6c537-289">In hello **Name** box, type **BrittaSimon**.</span></span>

   <span data-ttu-id="6c537-290">b.</span><span class="sxs-lookup"><span data-stu-id="6c537-290">b.</span></span> <span data-ttu-id="6c537-291">W hello **nazwy użytkownika** pole typu hello adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="6c537-291">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

   <span data-ttu-id="6c537-292">c.</span><span class="sxs-lookup"><span data-stu-id="6c537-292">c.</span></span> <span data-ttu-id="6c537-293">Wybierz hello **Pokaż hasło** pole wyboru, a następnie zapisz hello wartość, która jest wyświetlana w hello **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="6c537-293">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

   <span data-ttu-id="6c537-294">d.</span><span class="sxs-lookup"><span data-stu-id="6c537-294">d.</span></span> <span data-ttu-id="6c537-295">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="6c537-295">Click **Create**.</span></span>
 
### <a name="create-a-qlik-sense-enterprise-test-user"></a><span data-ttu-id="6c537-296">Tworzenie użytkownika testowego przedsiębiorstwa znaczeniu Qlik</span><span class="sxs-lookup"><span data-stu-id="6c537-296">Create a Qlik Sense Enterprise test user</span></span>

<span data-ttu-id="6c537-297">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w Qlik przedsiębiorstwa znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="6c537-297">In this section, you create a user called Britta Simon in Qlik Sense Enterprise.</span></span> <span data-ttu-id="6c537-298">Praca z [zespołem pomocy technicznej klienta przedsiębiorstwa znaczeniu Qlik](https://www.qlik.com/us/services/support) do dodawania użytkowników hello hello przedsiębiorstwa znaczeniu Qlik platformy.</span><span class="sxs-lookup"><span data-stu-id="6c537-298">Work with [Qlik Sense Enterprise Client support team](https://www.qlik.com/us/services/support) to add hello users in hello Qlik Sense Enterprise platform.</span></span> <span data-ttu-id="6c537-299">Użytkownicy muszą utworzyć i aktywowana, aby użyć rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="6c537-299">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="6c537-300">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="6c537-300">Assign hello Azure AD test user</span></span>

<span data-ttu-id="6c537-301">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooQlik przedsiębiorstwa znaczeniu.</span><span class="sxs-lookup"><span data-stu-id="6c537-301">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooQlik Sense Enterprise.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="6c537-303">**tooassign tooQlik Simona Britta przedsiębiorstwa znaczeniu, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="6c537-303">**tooassign Britta Simon tooQlik Sense Enterprise, perform hello following steps:**</span></span>

1. <span data-ttu-id="6c537-304">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="6c537-304">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="6c537-306">Z listy aplikacji hello wybierz **przedsiębiorstwa znaczeniu Qlik**.</span><span class="sxs-lookup"><span data-stu-id="6c537-306">In hello applications list, select **Qlik Sense Enterprise**.</span></span>

    ![łącze przedsiębiorstwa znaczeniu Qlik Hello na liście aplikacji hello](./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksense-enterprise_app.png)  

3. <span data-ttu-id="6c537-308">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="6c537-308">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202]

4. <span data-ttu-id="6c537-310">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="6c537-310">Click **Add** button.</span></span> <span data-ttu-id="6c537-311">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6c537-311">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="6c537-313">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="6c537-313">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="6c537-314">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6c537-314">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6c537-315">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="6c537-315">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="6c537-316">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="6c537-316">Test single sign-on</span></span>

<span data-ttu-id="6c537-317">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="6c537-317">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="6c537-318">Po kliknięciu kafelka przedsiębiorstwa znaczeniu Qlik hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour przedsiębiorstwa znaczeniu Qlik aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6c537-318">When you click hello Qlik Sense Enterprise tile in hello Access Panel, you should get automatically signed-on tooyour Qlik Sense Enterprise application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6c537-319">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="6c537-319">Additional resources</span></span>

* [<span data-ttu-id="6c537-320">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6c537-320">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6c537-321">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6c537-321">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_general_203.png

[qs6]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_06.png
[qs7]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_07.png
[qs8]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_08.png
[qs9]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_09.png
[qs10]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_10.png
[qs11]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_11.png
[qs12]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_12.png
[qs13]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_13.png
[qs14]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_14.png
[qs15]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_15.png
[qs16]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_16.png
[qs17]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_17.png
[qs18]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_18.png
[qs19]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_19.png
[qs20]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_20.png
[qs24]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_24.png
[qs51]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_51.png
[qs52]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_52.png
[qs53]: ./media/active-directory-saas-qliksense-enterprise-tutorial/tutorial_qliksenseenterprise_53.png

