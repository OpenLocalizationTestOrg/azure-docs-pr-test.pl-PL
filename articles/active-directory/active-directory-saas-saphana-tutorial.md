---
title: 'Samouczek: Integracji Azure Active Directory z SAP HANA | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i SAP HANA."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: 5ff6bfde0b1d7ab14025a4bc45199f9f826affd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a><span data-ttu-id="9f518-103">Samouczek: Integracji Azure Active Directory z SAP HANA</span><span class="sxs-lookup"><span data-stu-id="9f518-103">Tutorial: Azure Active Directory integration with SAP HANA</span></span>

<span data-ttu-id="9f518-104">Z tego samouczka, dowiesz się, jak toointegrate SAP HANA w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9f518-104">In this tutorial, you learn how toointegrate SAP HANA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9f518-105">Integrowanie SAP HANA z usługą Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="9f518-105">Integrating SAP HANA with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="9f518-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do tooSAP HANA</span><span class="sxs-lookup"><span data-stu-id="9f518-106">You can control in Azure AD who has access tooSAP HANA</span></span>
- <span data-ttu-id="9f518-107">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSAP HANA (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f518-107">You can enable your users tooautomatically get signed-on tooSAP HANA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9f518-108">Możesz zarządzać kont w jednej centralnej lokalizacji - hello portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9f518-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="9f518-109">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9f518-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9f518-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9f518-110">Prerequisites</span></span>

<span data-ttu-id="9f518-111">tooconfigure integracji z usługą Azure AD z SAP HANA należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="9f518-111">tooconfigure Azure AD integration with SAP HANA, you need hello following items:</span></span>

- <span data-ttu-id="9f518-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f518-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9f518-113">SAP HANA logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="9f518-113">A SAP HANA single sign-on enabled subscription</span></span>
- <span data-ttu-id="9f518-114">HANA uruchomione wystąpienie na publicznych IaaS, lokalnymi, maszynach wirtualnych platformy Azure lub SAP dużych wystąpień na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="9f518-114">A running HANA Instance either on any public IaaS, on-premises, Azure VMs or SAP Large Instances in Azure</span></span>
- <span data-ttu-id="9f518-115">Interfejs sieci Web administracji XSA Hello, jak również zainstalowana w wystąpieniu HANA hello Studio HANA.</span><span class="sxs-lookup"><span data-stu-id="9f518-115">hello XSA Administration Web Interface as well as HANA Studio installed on hello HANA instance.</span></span>

> [!NOTE]
> <span data-ttu-id="9f518-116">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego programu SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="9f518-116">tootest hello steps in this tutorial, we do not recommend using a production environment of SAP HANA.</span></span> <span data-ttu-id="9f518-117">Testowanie integracji hello najpierw w rozwoju lub przemieszczania środowisko aplikacji hello, a następnie środowiska produkcyjnego hello użycia.</span><span class="sxs-lookup"><span data-stu-id="9f518-117">Test hello integration first in development or staging environment of hello application and then use hello production environment.</span></span>

<span data-ttu-id="9f518-118">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="9f518-118">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9f518-119">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="9f518-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9f518-120">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9f518-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9f518-121">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="9f518-121">Scenario description</span></span>
<span data-ttu-id="9f518-122">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="9f518-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9f518-123">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="9f518-123">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9f518-124">Dodawanie SAP HANA z galerii hello</span><span class="sxs-lookup"><span data-stu-id="9f518-124">Adding SAP HANA from hello gallery</span></span>
2. <span data-ttu-id="9f518-125">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9f518-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-hana-from-hello-gallery"></a><span data-ttu-id="9f518-126">Dodawanie SAP HANA z galerii hello</span><span class="sxs-lookup"><span data-stu-id="9f518-126">Adding SAP HANA from hello gallery</span></span>
<span data-ttu-id="9f518-127">tooconfigure hello integracji SAP HANA do usługi Azure AD, należy tooadd SAP HANA z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="9f518-127">tooconfigure hello integration of SAP HANA into Azure AD, you need tooadd SAP HANA from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="9f518-128">**tooadd SAP HANA z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9f518-128">**tooadd SAP HANA from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f518-129">W hello  **[portalu Azure](https://portal.azure.com)**na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9f518-129">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![przycisk usługi Azure Active Directory Hello][1]

2. <span data-ttu-id="9f518-131">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="9f518-131">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="9f518-132">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9f518-132">Then go too**All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa Hello][2]
    
3. <span data-ttu-id="9f518-134">tooadd nową aplikację, kliknij przycisk **nowej aplikacji** przycisk u góry hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9f518-134">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nowy przycisk aplikacji Hello][3]

4. <span data-ttu-id="9f518-136">W polu wyszukiwania hello wpisz **SAP HANA**, wybierz pozycję **SAP HANA** z panelu wyników następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="9f518-136">In hello search box, type **SAP HANA**, select **SAP HANA** from result panel then click **Add** button tooadd hello application.</span></span> 

    ![Witaj nowej aplikacji](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9f518-138">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="9f518-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9f518-139">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SAP HANA oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="9f518-139">In this section, you configure and test Azure AD single sign-on with SAP HANA based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9f518-140">Dla pojedynczego logowania jednokrotnego toowork usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w SAP HANA jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f518-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP HANA is tooa user in Azure AD.</span></span> <span data-ttu-id="9f518-141">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w SAP HANA musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="9f518-141">In other words, a link relationship between an Azure AD user and hello related user in SAP HANA needs toobe established.</span></span>

<span data-ttu-id="9f518-142">Przypisywanie wartości hello hello SAP HANA **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** tooestablish hello łącze relacji.</span><span class="sxs-lookup"><span data-stu-id="9f518-142">In SAP HANA, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="9f518-143">tooconfigure i test usługi Azure AD rejestracji jednokrotnej z SAP HANA należy hello toocomplete po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="9f518-143">tooconfigure and test Azure AD single sign-on with SAP HANA, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="9f518-144">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="9f518-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="9f518-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="9f518-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9f518-146">**[Tworzenie użytkownika testowego SAP HANA](#creating-a-sap-hana-test-user)**  -toohave odpowiednikiem Simona Britta w SAP HANA, który jest połączony toohello usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9f518-146">**[Creating a SAP HANA test user](#creating-a-sap-hana-test-user)** - toohave a counterpart of Britta Simon in SAP HANA that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="9f518-147">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9f518-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9f518-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="9f518-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9f518-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9f518-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9f518-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w hello portalu Azure i skonfigurować logowanie jednokrotne w aplikacji SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="9f518-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP HANA application.</span></span>

<span data-ttu-id="9f518-151">**tooconfigure usługi Azure AD rejestracji jednokrotnej z SAP HANA wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="9f518-151">**tooconfigure Azure AD single sign-on with SAP HANA, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f518-152">W portalu Azure na powitania hello **SAP HANA** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="9f518-152">In hello Azure portal, on hello **SAP HANA** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="9f518-154">Na powitania **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** tooenable rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="9f518-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. <span data-ttu-id="9f518-156">Na powitania **adresy URL i SAP HANA domeny** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="9f518-156">On hello **SAP HANA Domain and URLs** section, perform hello following steps:</span></span>

    ![Domena i adres URL z jednym informacje logowania jednokrotnego](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    <span data-ttu-id="9f518-158">a.</span><span class="sxs-lookup"><span data-stu-id="9f518-158">a.</span></span> <span data-ttu-id="9f518-159">W hello **identyfikator** pole tekstowe, typu co:`HA100`</span><span class="sxs-lookup"><span data-stu-id="9f518-159">In hello **Identifier** textbox, type as: `HA100`</span></span> 

    <span data-ttu-id="9f518-160">b.</span><span class="sxs-lookup"><span data-stu-id="9f518-160">b.</span></span> <span data-ttu-id="9f518-161">W hello **adres URL odpowiedzi** tekstowym, wpisz adres URL za pomocą hello następującego wzorca:`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span><span class="sxs-lookup"><span data-stu-id="9f518-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9f518-162">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="9f518-162">These values are not real.</span></span> <span data-ttu-id="9f518-163">Witaj rzeczywisty identyfikator i odpowiedzi adresu URL, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="9f518-163">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="9f518-164">Skontaktuj się z [zespołem pomocy technicznej SAP HANA klienta](https://cloudplatform.sap.com/contact.html) tooget tych wartości.</span><span class="sxs-lookup"><span data-stu-id="9f518-164">Contact [SAP HANA Client support team](https://cloudplatform.sap.com/contact.html) tooget these values.</span></span> 

4. <span data-ttu-id="9f518-165">Na powitania **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="9f518-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![link do pobierania certyfikatu Hello](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    ><span data-ttu-id="9f518-167">Jeśli certyfikat nie jest aktywne następnie uaktywnić go, klikając hello wyboru "Utwórz nowy certyfikat active" w hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f518-167">If certificate is not active then make it active by clicking hello “Make new certificate active” checkbox in hello Azure AD.</span></span> 

5. <span data-ttu-id="9f518-168">Aplikacja SAP HANA oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="9f518-168">SAP HANA application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="9f518-169">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="9f518-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="9f518-170">W tym miejscu zostały zamapowane hello **identyfikator użytkownika** z **ExtractMailPrefix()** funkcji **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="9f518-170">Here we have mapped hello **User Identifier** with **ExtractMailPrefix()** function of **user.mail**.</span></span> <span data-ttu-id="9f518-171">Dzięki temu wartość prefiksu hello adres e-mail użytkownika hello, co jest hello Unikatowy identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9f518-171">This gives hello prefix value of email of hello user which is hello unique User ID.</span></span> <span data-ttu-id="9f518-172">Każdy odpowiedź oznaczająca Powodzenie to wysyłane toohello aplikacji SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="9f518-172">This is sent toohello SAP HANA application in every successful response.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. <span data-ttu-id="9f518-174">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego:</span><span class="sxs-lookup"><span data-stu-id="9f518-174">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="9f518-175">a.</span><span class="sxs-lookup"><span data-stu-id="9f518-175">a.</span></span> <span data-ttu-id="9f518-176">W hello **identyfikator użytkownika** listy rozwijanej wybierz **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="9f518-176">In hello **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>
    
    <span data-ttu-id="9f518-177">b.</span><span class="sxs-lookup"><span data-stu-id="9f518-177">b.</span></span> <span data-ttu-id="9f518-178">W hello **poczty** listy rozwijanej wybierz **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="9f518-178">In hello **Mail** dropdown list, select **user.mail**.</span></span>

7. <span data-ttu-id="9f518-179">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9f518-179">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="9f518-181">tooconfigure rejestracji jednokrotnej w **SAP HANA** strona, logowania tooyour **konsoli sieci Web XSA HANA** przechodząc toohello odpowiednich punkt końcowy HTTPS.</span><span class="sxs-lookup"><span data-stu-id="9f518-181">tooconfigure single sign-on on **SAP HANA** side, login tooyour **HANA XSA Web Console**  by browsing toohello respective HTTPS-endpoint.</span></span>

    > [!Note]
    > <span data-ttu-id="9f518-182">W konfiguracji domyślnej hello hello adresu URL przekierowuje ekran logowania tooa żądania hello, co wymaga poświadczeń hello uwierzytelnionego SAP HANA bazy danych toocomplete hello proces logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9f518-182">In hello default configuration, hello URL redirects hello request tooa logon screen, which requires hello credentials of an authenticated SAP HANA database user toocomplete hello logon process.</span></span> <span data-ttu-id="9f518-183">Witaj użytkownika, który loguje się musi mieć zadań administracyjnych hello uprawnienia wymagane tooperform SAML.</span><span class="sxs-lookup"><span data-stu-id="9f518-183">hello user who logs on must have hello privileges required tooperform SAML administration tasks.</span></span>

9. <span data-ttu-id="9f518-184">W hello XSA interfejs sieci Web, przejdź za**dostawca tożsamości SAML** i z tego miejsca, kliknij przycisk hello **"+"** -znajdujący się na dole hello hello ekranu toodisplay hello dodać informacje dostawcy tożsamości okienka i wykonania Witaj, następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9f518-184">In hello XSA Web Interface, navigate too**SAML Identity Provider** and from there, click hello **“+”** -button on hello bottom of hello screen toodisplay hello Add Identity Provider Info pane and perform hello following steps:</span></span>

    ![Dodaj dostawcę tożsamości](./media/active-directory-saas-saphana-tutorial/sap1.png)

    <span data-ttu-id="9f518-186">a.</span><span class="sxs-lookup"><span data-stu-id="9f518-186">a.</span></span> <span data-ttu-id="9f518-187">W hello **dodać informacje dostawcy tożsamości** okienka, Wklej zawartość hello hello XML metadanych, który został pobrany z portalu Azure, do hello **metadanych** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="9f518-187">In hello **Add Identity Provider Info** pane, paste hello contents of hello Metadata XML, which you have downloaded from Azure portal into hello **Metadata** textbox.</span></span>

    ![Dodaj ustawienia dostawcy tożsamości](./media/active-directory-saas-saphana-tutorial/sap2.png)

    <span data-ttu-id="9f518-189">b.</span><span class="sxs-lookup"><span data-stu-id="9f518-189">b.</span></span> <span data-ttu-id="9f518-190">Jeśli zawartość hello hello dokumentu XML są prawidłowe, proces analizowania hello wyodrębnia hello tooinsert informacje wymagane do hello **podmiotu, identyfikator jednostki i wystawcy** pól w hello ogólne dane obszar ekranu i hello pól adres URL w hello Obszar ekranu docelowy, na przykład  **podstawowego adresu URL i adresu URL SingleSignOn (*)**.</span><span class="sxs-lookup"><span data-stu-id="9f518-190">If hello contents of hello XML document are valid, hello parsing process extracts hello information required tooinsert into hello **Subject, Entity ID, and Issuer** fields in hello General Data screen area, and hello URL fields in hello Destination screen area, for example, **Base URL and SingleSignOn URL (*)**.</span></span>

    ![Dodaj ustawienia dostawcy tożsamości](./media/active-directory-saas-saphana-tutorial/sap3.png)

    <span data-ttu-id="9f518-192">c.</span><span class="sxs-lookup"><span data-stu-id="9f518-192">c.</span></span> <span data-ttu-id="9f518-193">W polu Nazwa hello hello danych ogólne obszar ekranu, wprowadź nazwę hello nowego logowania jednokrotnego SAML dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="9f518-193">In hello Name box of hello General Data screen area, enter a name for hello new SAML SSO identity provider.</span></span>

    > [!Note]
    > <span data-ttu-id="9f518-194">Nazwa Hello hello SAML IDP jest wymagana i musi być unikatowa. wygląda na to hello listę dostępnych IDPs SAML, który jest wyświetlany w przypadku wybrania SAML jako hello metodę uwierzytelniania dla programu SAP HANA XS toouse aplikacji, na przykład w obszarze ekranu uwierzytelniania hello narzędzia do administrowania artefaktu XS hello.</span><span class="sxs-lookup"><span data-stu-id="9f518-194">hello name of hello SAML IDP is mandatory and must be unique; it appears in hello list of available SAML IDPs that is displayed, if you select SAML as hello authentication method for SAP HANA XS applications toouse, for example, in hello Authentication screen area of hello XS Artifact Administration tool.</span></span>

10. <span data-ttu-id="9f518-195">Zapisz szczegóły hello hello nowy dostawca tożsamości SAML.</span><span class="sxs-lookup"><span data-stu-id="9f518-195">Save hello details of hello new SAML identity provider.</span></span> <span data-ttu-id="9f518-196">Wybierz **zapisać** toosave hello szczegóły dostawca tożsamości SAML hello i Dodaj hello nową SAML IDP toohello listę znanych IDPs SAML.</span><span class="sxs-lookup"><span data-stu-id="9f518-196">Choose **Save** toosave hello details of hello SAML identity provider and add hello new SAML IDP toohello list of known SAML IDPs.</span></span>

    ![Przyciskiem Zapisz](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. <span data-ttu-id="9f518-198">W Studio HANA w ramach właściwości systemu hello hello **konfiguracji** karcie, po prostu filtrowania ustawień przez **saml** i dostosować hello **assertion_timeout** z **10 s** za**120 s**.</span><span class="sxs-lookup"><span data-stu-id="9f518-198">In HANA Studio within hello system properties of hello **Configuration** tab, just filter settings by **saml** and adjust hello **assertion_timeout** from **10 sec** too**120 sec**.</span></span>

    ![Ustawienie assertion_timeout](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> <span data-ttu-id="9f518-200">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz hello [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji hello!</span><span class="sxs-lookup"><span data-stu-id="9f518-200">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="9f518-201">Po dodaniu tej aplikacji z hello **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij hello **rejestracji jednokrotnej** hello kartę i dostępu do osadzonych dokumentacji za pośrednictwem hello  **Konfiguracja** sekcji u dołu hello.</span><span class="sxs-lookup"><span data-stu-id="9f518-201">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="9f518-202">Więcej o hello osadzonych dokumentacji funkcji w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="9f518-202">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9f518-203">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f518-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="9f518-204">Celem Hello w tej sekcji jest toocreate użytkownika testowego, w portalu Azure o nazwie Simona Britta hello.</span><span class="sxs-lookup"><span data-stu-id="9f518-204">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="9f518-206">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9f518-206">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f518-207">W hello **portalu Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="9f518-207">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![przycisk usługi Azure Active Directory Hello](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9f518-209">toodisplay hello listę użytkowników, przejdź zbyt**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="9f518-209">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Witaj, "Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9f518-211">Witaj tooopen **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9f518-211">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![przycisk Dodaj Hello](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9f518-213">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9f518-213">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![okno dialogowe Hello użytkownika](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9f518-215">a.</span><span class="sxs-lookup"><span data-stu-id="9f518-215">a.</span></span> <span data-ttu-id="9f518-216">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9f518-216">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9f518-217">b.</span><span class="sxs-lookup"><span data-stu-id="9f518-217">b.</span></span> <span data-ttu-id="9f518-218">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9f518-218">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9f518-219">c.</span><span class="sxs-lookup"><span data-stu-id="9f518-219">c.</span></span> <span data-ttu-id="9f518-220">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="9f518-220">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="9f518-221">d.</span><span class="sxs-lookup"><span data-stu-id="9f518-221">d.</span></span> <span data-ttu-id="9f518-222">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="9f518-222">Click **Create**.</span></span>
 
### <a name="creating-a-sap-hana-test-user"></a><span data-ttu-id="9f518-223">Tworzenie użytkownika testowego SAP HANA</span><span class="sxs-lookup"><span data-stu-id="9f518-223">Creating a SAP HANA test user</span></span>

<span data-ttu-id="9f518-224">toolog użytkowników tooenable usługi Azure AD w tooSAP HANA muszą mieć przydzielone do programu SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="9f518-224">tooenable Azure AD users toolog in tooSAP HANA, they must be provisioned into SAP HANA.</span></span>
<span data-ttu-id="9f518-225">SAP HANA obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="9f518-225">SAP HANA supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="9f518-226">Jeśli potrzebujesz toocreate użytkownik ręcznie, wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="9f518-226">If you need toocreate a user manually, perform hello following steps:</span></span>

>[!Note]
><span data-ttu-id="9f518-227">Uwierzytelnianie zewnętrzne hello używane przez użytkownika hello, można zmienić.</span><span class="sxs-lookup"><span data-stu-id="9f518-227">You can change hello external authentication used by hello user.</span></span>
<span data-ttu-id="9f518-228">Użytkownicy zewnętrzni są uwierzytelniani, za pomocą zewnętrznego systemu, na przykład system protokołu Kerberos.</span><span class="sxs-lookup"><span data-stu-id="9f518-228">External users are authenticated using an external system, for example a Kerberos system.</span></span> <span data-ttu-id="9f518-229">Aby uzyskać szczegółowe informacje o tożsamości zewnętrznych, skontaktuj się z [administrator domeny](https://cloudplatform.sap.com/contact.html).</span><span class="sxs-lookup"><span data-stu-id="9f518-229">For detailed information about external identities, contact your [domain administrator](https://cloudplatform.sap.com/contact.html).</span></span>

1. <span data-ttu-id="9f518-230">Otwórz hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) jako administrator i Włącz hello bazy danych użytkownika dla logowania jednokrotnego SAML.</span><span class="sxs-lookup"><span data-stu-id="9f518-230">Open hello [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) as an administrator and enable hello DB-User for SAML SSO.</span></span>

    ![Utwórz użytkownika](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. <span data-ttu-id="9f518-232">Znaczników hello niewidoczne wyboru toohello rogu **SAML** i konfigurowanie hello łącza.</span><span class="sxs-lookup"><span data-stu-id="9f518-232">Tick hello invisible checkbox toohello left of **SAML** and follow hello Configure link.</span></span>

3. <span data-ttu-id="9f518-233">Kliknij przycisk **Dodaj** tooadd hello SAML IDP i kliknij przycisk **OK** wybranie hello odpowiednie IDP SAML.</span><span class="sxs-lookup"><span data-stu-id="9f518-233">Click **Add** tooadd hello SAML IDP and click **OK** selecting hello appropriate SAML IDP.</span></span>

4. <span data-ttu-id="9f518-234">Dodaj hello **tożsamości zewnętrznych** (np.</span><span class="sxs-lookup"><span data-stu-id="9f518-234">Add hello **External Identity** (ex.</span></span> <span data-ttu-id="9f518-235">W tym miejscu BrittaSimon) lub wybierz **"Wszystkie"** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="9f518-235">BrittaSimon here) or choose **"Any"** and click **OK**.</span></span>

    >[!Note]
    ><span data-ttu-id="9f518-236">Jeśli nie zaznaczono "Wszystkie" pole wyboru, a następnie hello nazwę użytkownika w HANA potrzebuje tooexactly dopasowania hello nazwy użytkownika hello w hello UPN przed sufiksem domeny hello (tj. BrittaSimon@contoso.com staje się BrittaSimon w HANA).</span><span class="sxs-lookup"><span data-stu-id="9f518-236">If "ANY" check-box is not checked, then hello user name in HANA needs tooexactly match hello name of hello user in hello UPN before hello domain suffix (i.e. BrittaSimon@contoso.com would become BrittaSimon in HANA).</span></span>

5. <span data-ttu-id="9f518-237">Do celów testowych, przypisać wszystkie **"XS"** użytkownika toohello ról.</span><span class="sxs-lookup"><span data-stu-id="9f518-237">For testing purposes, assign all **"XS"** roles toohello user.</span></span>

    ![Przypisywanie ról](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > <span data-ttu-id="9f518-239">Należy podać te uprawnienia, które są odpowiednie dla Twojej przypadki użycia tylko.</span><span class="sxs-lookup"><span data-stu-id="9f518-239">You should give those permissions appropriate for your use cases, only.</span></span>

6. <span data-ttu-id="9f518-240">Zapisz hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="9f518-240">Save hello user.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="9f518-241">Przypisanie użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="9f518-241">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="9f518-242">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie dostępu tooSAP HANA.</span><span class="sxs-lookup"><span data-stu-id="9f518-242">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP HANA.</span></span>

![Przypisanie roli użytkownika hello][200] 

<span data-ttu-id="9f518-244">**tooassign tooSAP Simona Britta HANA, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="9f518-244">**tooassign Britta Simon tooSAP HANA, perform hello following steps:**</span></span>

1. <span data-ttu-id="9f518-245">W portalu Azure hello, otwórz widok aplikacji hello, a następnie przejdź do widoku katalogu toohello i przejść za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="9f518-245">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="9f518-247">Z listy aplikacji hello wybierz **SAP HANA**.</span><span class="sxs-lookup"><span data-stu-id="9f518-247">In hello applications list, select **SAP HANA**.</span></span>

    ![Przypisz użytkownika](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. <span data-ttu-id="9f518-249">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="9f518-249">In hello menu on hello left, click **Users and groups**.</span></span>

    ![łącze "Użytkownicy i grupy" Hello][202] 

4. <span data-ttu-id="9f518-251">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="9f518-251">Click **Add** button.</span></span> <span data-ttu-id="9f518-252">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9f518-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Okienko Dodaj przypisania Hello][203]

5. <span data-ttu-id="9f518-254">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="9f518-254">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="9f518-255">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9f518-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9f518-256">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="9f518-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9f518-257">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="9f518-257">Testing single sign-on</span></span>

<span data-ttu-id="9f518-258">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania jednokrotnego przy użyciu hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="9f518-258">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="9f518-259">Po kliknięciu kafelka SAP HANA hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour aplikacji SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="9f518-259">When you click hello SAP HANA tile in hello Access Panel, you should get automatically signed-on tooyour SAP HANA application.</span></span>
<span data-ttu-id="9f518-260">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9f518-260">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9f518-261">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="9f518-261">Additional resources</span></span>

* [<span data-ttu-id="9f518-262">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9f518-262">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9f518-263">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9f518-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png

