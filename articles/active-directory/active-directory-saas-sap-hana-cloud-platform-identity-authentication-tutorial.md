---
title: "Samouczek: Integracji Azure Active Directory z uwierzytelnianie tożsamości SAP HANA chmury platformy | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure logowanie jednokrotne między usługą Azure Active Directory i SAP HANA Cloud Platform tożsamość uwierzytelniania."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1c1320d1-7ba4-4b5f-926f-4996b44d9b5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: 2142770779ddb745555b47fc85b5457b573f9506
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform-identity-authentication"></a><span data-ttu-id="0dea2-103">Samouczek: Integracji Azure Active Directory z uwierzytelnianie tożsamości SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="0dea2-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform Identity Authentication</span></span>

<span data-ttu-id="0dea2-104">Z tego samouczka, dowiesz się, jak toointegrate SAP HANA chmury platformy tożsamość uwierzytelniania za pomocą usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0dea2-104">In this tutorial, you learn how toointegrate SAP HANA Cloud Platform Identity Authentication with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="0dea2-105">Uwierzytelnianie tożsamości SAP HANA Cloud Platform jest używana jako serwera proxy IdP tooaccess SAP aplikacji przy użyciu usługi Azure AD jako hello IdP głównego.</span><span class="sxs-lookup"><span data-stu-id="0dea2-105">SAP HANA Cloud Platform Identity Authentication is used as a proxy IdP tooaccess SAP applications using Azure AD as hello main IdP.</span></span>

<span data-ttu-id="0dea2-106">Integrowanie SAP HANA Cloud Platform tożsamości uwierzytelniania z usługi Azure AD zapewnia hello następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="0dea2-106">Integrating SAP HANA Cloud Platform Identity Authentication with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0dea2-107">Można kontrolować w usłudze Azure AD, kto ma dostęp do aplikacji tooSAP</span><span class="sxs-lookup"><span data-stu-id="0dea2-107">You can control in Azure AD who has access tooSAP application</span></span>
- <span data-ttu-id="0dea2-108">Można włączyć użytkownika użytkownicy tooautomatically get zalogowane tooSAP aplikacji rejestracji jednokrotnej (SSO) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dea2-108">You can enable your users tooautomatically get signed-on tooSAP applications single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="0dea2-109">Możesz zarządzać kont w jednej centralnej lokalizacji - hello klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="0dea2-109">You can manage your accounts in one central location - hello Azure classic portal</span></span>

<span data-ttu-id="0dea2-110">Jeśli chcesz tooknow więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0dea2-110">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="0dea2-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="0dea2-111">Prerequisites</span></span>

<span data-ttu-id="0dea2-112">tooconfigure integracji usługi Azure AD z uwierzytelnianie tożsamości SAP HANA Cloud Platform, należy hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="0dea2-112">tooconfigure Azure AD integration with SAP HANA Cloud Platform Identity Authentication, you need hello following items:</span></span>

- <span data-ttu-id="0dea2-113">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dea2-113">An Azure AD subscription</span></span>
- <span data-ttu-id="0dea2-114">A **uwierzytelnianie tożsamości SAP HANA Cloud Platform** logowanie Jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="0dea2-114">A **SAP HANA Cloud Platform Identity Authentication** SSO enabled subscription</span></span>


>[!NOTE] 
><span data-ttu-id="0dea2-115">tootest hello kroków w tym samouczku, zaleca się przy użyciu środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="0dea2-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="0dea2-116">tootest hello kroki opisane w tym samouczku, należy stosować te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="0dea2-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0dea2-117">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="0dea2-117">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="0dea2-118">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0dea2-118">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0dea2-119">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="0dea2-119">Scenario description</span></span>
<span data-ttu-id="0dea2-120">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="0dea2-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="0dea2-121">Scenariusz Hello opisane w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="0dea2-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0dea2-122">Dodawanie uwierzytelniania tożsamości SAP HANA chmury platformy z galerii hello</span><span class="sxs-lookup"><span data-stu-id="0dea2-122">Adding SAP HANA Cloud Platform Identity Authentication from hello gallery</span></span>
2. <span data-ttu-id="0dea2-123">Konfigurowanie i testowania logowania jednokrotnego programu Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dea2-123">Configuring and testing Azure AD SSO</span></span>

<span data-ttu-id="0dea2-124">Przed rozpoczęciem pracy hello szczegółowe informacje techniczne, jest istotne toounderstand hello pojęcia, które chcesz zacząć toolook w.</span><span class="sxs-lookup"><span data-stu-id="0dea2-124">Before diving into hello technical details, it is vital toounderstand hello concepts you're going toolook at.</span></span> <span data-ttu-id="0dea2-125">Witaj uwierzytelnianie tożsamości SAP HANA Cloud Platform i Azure Active Directory federation umożliwia tooimplement logowania jednokrotnego w aplikacji lub usług chronione przez usługi AAD (jako IdP) przy użyciu aplikacje SAP i chronione przez SAP HANA Cloud Platform tożsamości usługi Uwierzytelnianie.</span><span class="sxs-lookup"><span data-stu-id="0dea2-125">hello SAP HANA Cloud Platform Identity Authentication and Azure Active Directory federation enables you tooimplement SSO across applications or services protected by AAD (as an IdP) with SAP applications and services protected by SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="0dea2-126">Obecnie uwierzytelnianie tożsamości SAP HANA Cloud Platform działa jako dostawca tożsamości serwera Proxy tooSAP — aplikacje.</span><span class="sxs-lookup"><span data-stu-id="0dea2-126">Currently, SAP HANA Cloud Platform Identity Authentication acts as a Proxy Identity Provider tooSAP-applications.</span></span> <span data-ttu-id="0dea2-127">Usługa Azure Active Directory z kolei działa jako hello wiodące dostawcy tożsamości w tej instalacji.</span><span class="sxs-lookup"><span data-stu-id="0dea2-127">Azure Active Directory in turn acts as hello leading Identity Provider in this setup.</span></span> 

<span data-ttu-id="0dea2-128">powitania po diagram ilustruje to:</span><span class="sxs-lookup"><span data-stu-id="0dea2-128">hello following diagram illustrates this:</span></span>    

![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/architecture-01.png)

<span data-ttu-id="0dea2-130">W przypadku tej konfiguracji dzierżawy uwierzytelnianie tożsamości SAP HANA Cloud Platform zostanie skonfigurowany jako zaufanych aplikacji w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0dea2-130">With this setup, your SAP HANA Cloud Platform Identity Authentication tenant will be configured as a trusted application in Azure Active Directory.</span></span> 

<span data-ttu-id="0dea2-131">Wszystkie aplikacje SAP i usługi mają tooprotect za pośrednictwem w ten sposób następnie są konfigurowane w konsoli zarządzania uwierzytelnianie tożsamości SAP HANA Cloud Platform hello!</span><span class="sxs-lookup"><span data-stu-id="0dea2-131">All SAP applications and services you want tooprotect through this way are subsequently configured in hello SAP HANA Cloud Platform Identity Authentication management console!</span></span>

<span data-ttu-id="0dea2-132">To oznacza, że autoryzacji za udzielanie dostępu tooSAP aplikacji i usług potrzeb tootake miejscu uwierzytelnianie tożsamości SAP HANA Cloud Platform dla instalacji (w przeciwieństwie tooconfiguring autoryzacji w usłudze Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="0dea2-132">This means that authorization for granting access tooSAP applications and services needs tootake place in SAP HANA Cloud Platform Identity Authentication for such a setup (as opposed tooconfiguring authorization in Azure Active Directory).</span></span>

<span data-ttu-id="0dea2-133">Konfigurując uwierzytelnianie tożsamości SAP HANA chmury platformy jako aplikację za pomocą hello Azure Active Directory Marketplace, nie potrzebujesz tootake nad Konfigurowanie wymagane oddzielne oświadczenia / tooproduce potrzebne potwierdzenia języka SAML i przekształcenia token uwierzytelniania prawidłowy dla aplikacji SAP.</span><span class="sxs-lookup"><span data-stu-id="0dea2-133">By configuring SAP HANA Cloud Platform Identity Authentication as an application through hello Azure Active Directory Marketplace, you don't need tootake care of configuring needed individual claims / SAML assertions and transformations needed tooproduce a valid authentication token for SAP applications.</span></span>

>[!NOTE] 
><span data-ttu-id="0dea2-134">Obecnie obie strony tylko przetestowano Jednokrotną w sieci Web.</span><span class="sxs-lookup"><span data-stu-id="0dea2-134">Currently Web SSO has been tested by both parties, only.</span></span> <span data-ttu-id="0dea2-135">Przepływy potrzebne w przypadku aplikacji do interfejsu API lub interfejsu API do interfejsu API komunikacji powinny działać, ale nie zostały one przetestowane, jeszcze.</span><span class="sxs-lookup"><span data-stu-id="0dea2-135">Flows needed for App-to-API or API-to-API communication should work but have not been tested, yet.</span></span> <span data-ttu-id="0dea2-136">Zostaną one przetestowane w ramach kolejnych działań.</span><span class="sxs-lookup"><span data-stu-id="0dea2-136">They will be tested as part of subsequent activities.</span></span>
>

## <a name="add-sap-hana-cloud-platform-identity-authentication-from-hello-gallery"></a><span data-ttu-id="0dea2-137">Dodaj uwierzytelnianie tożsamości SAP HANA Cloud Platform z galerii hello</span><span class="sxs-lookup"><span data-stu-id="0dea2-137">Add SAP HANA Cloud Platform Identity Authentication from hello gallery</span></span>
<span data-ttu-id="0dea2-138">tooconfigure hello integracji SAP HANA Cloud Platform tożsamości uwierzytelniania w usłudze Azure Active Directory, należy tooadd uwierzytelnianie tożsamości SAP HANA Cloud Platform z hello galerii tooyour listę zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="0dea2-138">tooconfigure hello integration of SAP HANA Cloud Platform Identity Authentication into Azure AD, you need tooadd SAP HANA Cloud Platform Identity Authentication from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0dea2-139">**tooadd SAP HANA platformy tożsamość uwierzytelniania w chmurze z galerii hello, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0dea2-139">**tooadd SAP HANA Cloud Platform Identity Authentication from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dea2-140">W hello [ **portalu zarządzania Azure**](https://portal.azure.com)na temat hello panelu nawigacji po lewej stronie, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0dea2-140">In hello [**Azure Management portal**](https://portal.azure.com), on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="0dea2-142">Przejdź za**aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="0dea2-142">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0dea2-143">Następnie przejdź zbyt**wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0dea2-143">Then go too**All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="0dea2-145">Kliknij przycisk **Dodaj** przycisk u góry hello hello okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0dea2-145">Click **Add** button on hello top of hello dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="0dea2-147">W polu wyszukiwania hello wpisz **uwierzytelnianie tożsamości SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="0dea2-147">In hello search box, type **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_01.png)

5. <span data-ttu-id="0dea2-149">W panelu wyników hello, wybierz **uwierzytelnianie tożsamości SAP HANA Cloud Platform**, a następnie kliknij przycisk **Dodaj** przycisk aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="0dea2-149">In hello results panel, select **SAP HANA Cloud Platform Identity Authentication**, and then click **Add** button tooadd hello application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_02.png)


##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0dea2-151">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0dea2-151">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="0dea2-152">W tej sekcji możesz Konfiguracja i testowanie usługi Azure AD SSO z SAP HANA Cloud Platform tożsamości uwierzytelnianie oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="0dea2-152">In this section, you configure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0dea2-153">Aby toowork logowania jednokrotnego usługi Azure AD musi tooknow użytkownika odpowiednikiem hello w SAP HANA Cloud Platform tożsamości uwierzytelniania jest tooa użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0dea2-153">For SSO toowork, Azure AD needs tooknow what hello counterpart user in SAP HANA Cloud Platform Identity Authentication is tooa user in Azure AD.</span></span> <span data-ttu-id="0dea2-154">Innymi słowy relację łącza między użytkownika usługi Azure AD i hello użytkownikowi w uwierzytelnianie tożsamości SAP HANA chmury platformy musi toobe ustanowione.</span><span class="sxs-lookup"><span data-stu-id="0dea2-154">In other words, a link relationship between an Azure AD user and hello related user in SAP HANA Cloud Platform Identity Authentication needs toobe established.</span></span>

<span data-ttu-id="0dea2-155">Ta relacja łącza zostanie nawiązane, przypisując wartość hello hello **nazwy użytkownika** w usłudze Azure AD jako wartość hello hello **Username** w uwierzytelnianie tożsamości SAP HANA chmury platformy.</span><span class="sxs-lookup"><span data-stu-id="0dea2-155">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in SAP HANA Cloud Platform Identity Authentication.</span></span>

<span data-ttu-id="0dea2-156">tooconfigure i testowania Azure AD z logowania jednokrotnego SAP HANA Cloud Platform tożsamości uwierzytelniania, należy po bloków konstrukcyjnych hello toocomplete:</span><span class="sxs-lookup"><span data-stu-id="0dea2-156">tooconfigure and test Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0dea2-157">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  -tooenable Twojego toouse użytkowników tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="0dea2-157">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0dea2-158">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  -tootest usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0dea2-158">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0dea2-159">**[Tworzenie użytkownika testowego uwierzytelnianie tożsamości SAP HANA Cloud Platform](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)**  -toohave odpowiednikiem Simona Britta w SAP HANA chmury platformy tożsamości uwierzytelniania, który jest jego reprezentacja toohello połączonej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0dea2-159">**[Creating a SAP HANA Cloud Platform Identity Authentication test user](#creating-a-sap-hana-cloud-platform-identity-authentication-test-user)** - toohave a counterpart of Britta Simon in SAP HANA Cloud Platform Identity Authentication that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="0dea2-160">**[Przypisanie użytkownika testowego hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Simona Britta toouse usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="0dea2-160">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0dea2-161">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  -tooverify czy hello konfiguracji działania.</span><span class="sxs-lookup"><span data-stu-id="0dea2-161">**[Testing single sign-on](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-sso"></a><span data-ttu-id="0dea2-162">Konfigurowanie usługi Azure AD logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="0dea2-162">Configuring Azure AD SSO</span></span>

<span data-ttu-id="0dea2-163">W tej sekcji włączenia funkcji logowania jednokrotnego usługi Azure AD w portalu zarządzania Azure hello i skonfigurować logowanie jednokrotne do aplikacji uwierzytelnianie tożsamości SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="0dea2-163">In this section, you enable Azure AD SSO in hello Azure Management portal and configure single sign-on in your SAP HANA Cloud Platform Identity Authentication application.</span></span>

<span data-ttu-id="0dea2-164">Uwierzytelnianie tożsamości SAP HANA chmury platformy aplikacji oczekuje potwierdzenia SAML hello w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="0dea2-164">SAP HANA Cloud Platform Identity Authentication application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="0dea2-165">Można zarządzać hello wartości tych atrybutów z hello "**atrybuty użytkownika**" sekcji na stronie integracji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0dea2-165">You can manage hello values of these attributes from hello "**User Attributes**" section on application integration page.</span></span> <span data-ttu-id="0dea2-166">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="0dea2-166">hello following screenshot shows an example for this.</span></span>

![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_03.png)

<span data-ttu-id="0dea2-168">**tooconfigure Azure AD SSO z SAP HANA platformy tożsamość uwierzytelniania w chmurze, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0dea2-168">**tooconfigure Azure AD SSO with SAP HANA Cloud Platform Identity Authentication, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dea2-169">W portalu zarządzania Azure hello na powitania **uwierzytelnianie tożsamości SAP HANA Cloud Platform** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="0dea2-169">In hello Azure Management portal, on hello **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="0dea2-171">Na powitania **logowanie jednokrotne** okna dialogowego, jako **tryb** wybierz **na języku SAML logowania jednokrotnego** tooenable logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="0dea2-171">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej][5]

3. <span data-ttu-id="0dea2-173">W hello **atrybuty użytkownika** sekcji na powitania **logowanie jednokrotne** okna dialogowego, jeśli aplikacja SAP oczekuje na przykład "imię" atrybutu.</span><span class="sxs-lookup"><span data-stu-id="0dea2-173">In hello **User Attributes** section on hello **Single sign-on** dialog, if your SAP application expects an attribute for example "firstName".</span></span> <span data-ttu-id="0dea2-174">W oknie dialogowym atrybuty tokenu SAML hello Dodaj atrybut "imię" hello.</span><span class="sxs-lookup"><span data-stu-id="0dea2-174">On hello SAML token attributes dialog, add hello "firstName" attribute.</span></span>
 1. <span data-ttu-id="0dea2-175">Kliknij przycisk **Dodaj atrybut** tooopen hello **Dodawanie atrybutu** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0dea2-175">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej][6]

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_05.png)
 2. <span data-ttu-id="0dea2-178">W hello **nazwa atrybutu** pole tekstowe, nazwa atrybutu hello typu "imię".</span><span class="sxs-lookup"><span data-stu-id="0dea2-178">In hello **Attribute Name** textbox, type hello attribute name "firstName".</span></span>
 3. <span data-ttu-id="0dea2-179">Z hello **wartość atrybutu** listy, wybierz opcję hello wartość atrybutu "user.givenname".</span><span class="sxs-lookup"><span data-stu-id="0dea2-179">From hello **Attribute Value** list, select hello attribute value "user.givenname".</span></span>
 4. <span data-ttu-id="0dea2-180">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="0dea2-180">Click **Ok**.</span></span>

4. <span data-ttu-id="0dea2-181">Na powitania **adresy URL i domeny uwierzytelniania tożsamości chmury platformy SAP HANA** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="0dea2-181">On hello **SAP HANA Cloud Platform Identity Authentication Domain and URLs** section, perform hello following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_06.png)
 1. <span data-ttu-id="0dea2-183">W hello **na adres URL logowania** tekstowym, wpisz znak hello na adres URL dla aplikacji SAP hello.</span><span class="sxs-lookup"><span data-stu-id="0dea2-183">In hello **Sign On URL** textbox, type hello sign on URL for hello SAP application.</span></span>
 2. <span data-ttu-id="0dea2-184">W hello **identyfikator** pole tekstowe, wartość hello typu następującego wzorca:`<entity-id>.accounts.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="0dea2-184">In hello **Identifier** textbox, type hello value following pattern: `<entity-id>.accounts.ondemand.com`</span></span> 
    * <span data-ttu-id="0dea2-185">Jeśli nie znasz tej wartości, wykonaj hello uwierzytelnianie tożsamości SAP HANA Cloud Platform dokumentacji [dzierżawy SAML 2.0 konfiguracji](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span><span class="sxs-lookup"><span data-stu-id="0dea2-185">If you don't know this value, please follow hello SAP HANA Cloud Platform Identity Authentication documentation on [Tenant SAML 2.0 Configuration](https://help.hana.ondemand.com/cloud_identity/frameset.htm?e81a19b0067f4646982d7200a8dab3ca.html).</span></span>

5. <span data-ttu-id="0dea2-186">Na powitania **konfiguracji uwierzytelniania tożsamości chmury platformy SAP HANA** kliknij **skonfigurować SAP HANA platformy tożsamość uwierzytelniania w chmurze** tooopen **Konfigurowanie logowania jednokrotnego** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0dea2-186">On hello **SAP HANA Cloud Platform Identity Authentication Configuration** section, click **Configure SAP HANA Cloud Platform Identity Authentication** tooopen **Configure sign-on** dialog.</span></span> <span data-ttu-id="0dea2-187">Następnie kliknij **SAML XML metadanych** i Zapisz plik hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="0dea2-187">Then, click on **SAML XML Metadata** and save hello file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_07.png) 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_08.png)

6. <span data-ttu-id="0dea2-190">tooget logowania jednokrotnego skonfigurowane dla danej aplikacji, przejdź tooSAP konsoli administracyjnej uwierzytelniania tożsamości HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="0dea2-190">tooget SSO configured for your application, go tooSAP HANA Cloud Platform Identity Authentication Administration Console.</span></span> <span data-ttu-id="0dea2-191">adres URL Hello ma hello następującego wzorca:`https://<tenant-id>.accounts.ondemand.com/admin`</span><span class="sxs-lookup"><span data-stu-id="0dea2-191">hello URL has hello following pattern: `https://<tenant-id>.accounts.ondemand.com/admin`</span></span>
 * <span data-ttu-id="0dea2-192">Następnie wykonaj dokumentacji hello na uwierzytelnianie tożsamości SAP HANA Cloud Platform zbyt[Konfigurowanie usługi Microsoft Azure AD jako firmowe dostawcy tożsamości na uwierzytelnianie tożsamości SAP HANA Cloud Platform](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span><span class="sxs-lookup"><span data-stu-id="0dea2-192">Then, follow hello documentation on SAP HANA Cloud Platform Identity Authentication too[Configure Microsoft Azure AD as Corporate Identity Provider at SAP HANA Cloud Platform Identity Authentication](https://help.hana.ondemand.com/cloud_identity/frameset.htm?626b17331b4d4014b8790d3aea70b240.html).</span></span> 

7. <span data-ttu-id="0dea2-193">W portalu zarządzania Azure powitania kliknij **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0dea2-193">In hello Azure Management portal, click **Save** button.</span></span>
8. <span data-ttu-id="0dea2-194">Nadal hello następujące kroki tylko wtedy, gdy mają tooadd i włączenia funkcji logowania jednokrotnego dla innej aplikacji SAP.</span><span class="sxs-lookup"><span data-stu-id="0dea2-194">Continue hello following steps only if you want tooadd and enable SSO for another SAP application.</span></span> <span data-ttu-id="0dea2-195">Powtórz kroki w obszarze hello sekcję "Dodawanie SAP HANA platformy tożsamość uwierzytelniania w chmurze z galerii hello" tooadd inne wystąpienie programu SAP HANA Cloud Platform tożsamości uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="0dea2-195">Repeat steps under hello section “Adding SAP HANA Cloud Platform Identity Authentication from hello gallery” tooadd another instance of SAP HANA Cloud Platform Identity Authentication.</span></span>
9. <span data-ttu-id="0dea2-196">W portalu zarządzania Azure hello na powitania **uwierzytelnianie tożsamości SAP HANA Cloud Platform** strona integracji aplikacji, kliknij przycisk **połączonej logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="0dea2-196">In hello Azure Management portal, on hello **SAP HANA Cloud Platform Identity Authentication** application integration page, click **Linked Sign-on**.</span></span>

    ![Skonfiguruj połączonego logowania jednokrotnego](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/linked_sign_on.png)
10. <span data-ttu-id="0dea2-198">Następnie Zapisz konfigurację hello.</span><span class="sxs-lookup"><span data-stu-id="0dea2-198">Then, save hello configuration.</span></span>

>[!NOTE] 
><span data-ttu-id="0dea2-199">Nowa aplikacja Hello będzie korzystać z konfiguracji logowania jednokrotnego hello hello poprzedniej SAP aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0dea2-199">hello new application will leverage hello SSO configuration for hello previous SAP application.</span></span> <span data-ttu-id="0dea2-200">Upewnij się, możesz Użyj hello tej samej firmowej dostawców tożsamości w hello konsoli administracyjnej uwierzytelniania tożsamości platformy SAP HANA chmury.</span><span class="sxs-lookup"><span data-stu-id="0dea2-200">Please make sure you use hello same Corporate Identity Providers in hello SAP HANA Cloud Platform Identity Authentication Administration Console.</span></span>
>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0dea2-201">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dea2-201">Create an Azure AD test user</span></span>
<span data-ttu-id="0dea2-202">Celem Hello w tej sekcji jest toocreate użytkownika testowego w hello nowego portalu o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="0dea2-202">hello objective of this section is toocreate a test user in hello new portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="0dea2-204">**toocreate użytkownika testowego w usłudze Azure AD, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="0dea2-204">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dea2-205">W hello **portalu zarządzania Azure**na temat hello w lewym okienku nawigacji, kliknij przycisk **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="0dea2-205">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0dea2-207">Przejdź za**użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy** toodisplay hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0dea2-207">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0dea2-209">U góry okna dialogowego hello powitania kliknij **Dodaj** tooopen hello **użytkownika** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0dea2-209">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0dea2-211">Na powitania **użytkownika** okna dialogowego wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="0dea2-211">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/create_aaduser_04.png) 
  1. <span data-ttu-id="0dea2-213">W hello **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0dea2-213">In hello **Name** textbox, type **BrittaSimon**.</span></span>
  2. <span data-ttu-id="0dea2-214">W hello **nazwy użytkownika** pole tekstowe, hello typu **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0dea2-214">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>
  3. <span data-ttu-id="0dea2-215">Wybierz **Pokaż hasło** i zanotuj wartość hello hello **hasło**.</span><span class="sxs-lookup"><span data-stu-id="0dea2-215">Select **Show Password** and write down hello value of hello **Password**.</span></span>
  4. <span data-ttu-id="0dea2-216">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="0dea2-216">Click **Create**.</span></span> 

### <a name="create-a-sap-hana-cloud-platform-identity-authentication-test-user"></a><span data-ttu-id="0dea2-217">Tworzenie użytkownika testowego uwierzytelnianie tożsamości SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="0dea2-217">Create a SAP HANA Cloud Platform Identity Authentication test user</span></span>

<span data-ttu-id="0dea2-218">Nie trzeba toocreate użytkownika na uwierzytelnianie tożsamości SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="0dea2-218">You don't need toocreate an user on SAP HANA Cloud Platform Identity Authentication.</span></span> <span data-ttu-id="0dea2-219">Użytkownicy, którzy są w magazynie użytkownika hello Azure AD można użyć funkcji logowania jednokrotnego hello.</span><span class="sxs-lookup"><span data-stu-id="0dea2-219">Users who are in hello Azure AD user store can use hello SSO functionality.</span></span>

<span data-ttu-id="0dea2-220">Uwierzytelnianie tożsamości SAP HANA chmurze platforma obsługuje hello opcję federacji tożsamości.</span><span class="sxs-lookup"><span data-stu-id="0dea2-220">SAP HANA Cloud Platform Identity Authentication supports hello Identity Federation option.</span></span> <span data-ttu-id="0dea2-221">Ta opcja umożliwia toocheck aplikacji hello, jeśli użytkownik hello uwierzytelniony przez dostawcę tożsamości firmy hello w hello użytkownika magazynu programu SAP HANA platformy tożsamość uwierzytelniania w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0dea2-221">This option allows hello application toocheck if hello users authenticated by hello corporate identity provider exist in hello user store of SAP HANA Cloud Platform Identity Authentication.</span></span> 

<span data-ttu-id="0dea2-222">W ustawieniu domyślny hello, hello opcja federacji tożsamości jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="0dea2-222">In hello default setting, hello Identity Federation option is disabled.</span></span> <span data-ttu-id="0dea2-223">Włączenie federacji tożsamości tylko użytkownicy hello zaimportowane w SAP HANA Cloud Platform tożsamości uwierzytelniania są aplikacji hello tooaccess stanie.</span><span class="sxs-lookup"><span data-stu-id="0dea2-223">If Identity Federation is enabled, only hello users that are imported in SAP HANA Cloud Platform Identity Authentication are able tooaccess hello application.</span></span> 

<span data-ttu-id="0dea2-224">Aby uzyskać więcej informacji na temat tooenable lub wyłącz federacji tożsamości z SAP HANA platformy tożsamość uwierzytelniania w chmurze, zobacz temat włączyć Federację tożsamości z SAP HANA platformy tożsamość uwierzytelniania w chmurze w [Konfigurowanie federacji tożsamości z hello użytkownika magazynu programu SAP HANA platformy tożsamość uwierzytelniania w chmurze. ](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span><span class="sxs-lookup"><span data-stu-id="0dea2-224">For more information about how tooenable or disable Identity Federation with SAP HANA Cloud Platform Identity Authentication, see Enable Identity Federation with SAP HANA Cloud Platform Identity Authentication in [Configure Identity Federation with hello User Store of SAP HANA Cloud Platform Identity Authentication.](https://help.hana.ondemand.com/cloud_identity/frameset.htm?c029bbbaefbf4350af15115396ba14e2.html).</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="0dea2-225">Przypisz użytkownika testowego hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0dea2-225">Assign hello Azure AD test user</span></span>

<span data-ttu-id="0dea2-226">W tej sekcji możesz włączyć toouse Simona Britta Azure logowania jednokrotnego za udzielanie jej tooSAP dostęp do uwierzytelniania tożsamości platformy HANA w chmurze.</span><span class="sxs-lookup"><span data-stu-id="0dea2-226">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooSAP HANA Cloud Platform Identity Authentication.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="0dea2-228">**tooassign tooSAP Simona Britta HANA uwierzytelnianie tożsamości platformy chmury, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="0dea2-228">**tooassign Britta Simon tooSAP HANA Cloud Platform Identity Authentication, perform hello following steps:**</span></span>

1. <span data-ttu-id="0dea2-229">W portalu zarządzania Azure hello, otwórz widok aplikacji hello, a następnie przejdź widok katalogu toohello i go za**aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="0dea2-229">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="0dea2-231">Z listy aplikacji hello wybierz **uwierzytelnianie tożsamości SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="0dea2-231">In hello applications list, select **SAP HANA Cloud Platform Identity Authentication**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_sap_cloud_identity_09.png)

3. <span data-ttu-id="0dea2-233">W menu powitania po lewej stronie powitania kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="0dea2-233">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="0dea2-235">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="0dea2-235">Click **Add** button.</span></span> <span data-ttu-id="0dea2-236">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0dea2-236">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="0dea2-238">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** hello listy użytkowników.</span><span class="sxs-lookup"><span data-stu-id="0dea2-238">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0dea2-239">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0dea2-239">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0dea2-240">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="0dea2-240">Click **Assign** button on **Add Assignment** dialog.</span></span>
    

### <a name="test-single-sign-on"></a><span data-ttu-id="0dea2-241">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="0dea2-241">Test single sign-on</span></span>

<span data-ttu-id="0dea2-242">W tej sekcji można przetestować konfigurację usługi Azure AD z logowania jednokrotnego za pomocą hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="0dea2-242">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="0dea2-243">Po kliknięciu kafelka uwierzytelnianie tożsamości SAP HANA Cloud Platform hello w hello Panel dostępu, należy pobrać automatycznie zalogowane tooyour uwierzytelnianie tożsamości SAP HANA Cloud Platform aplikacji.</span><span class="sxs-lookup"><span data-stu-id="0dea2-243">When you click hello SAP HANA Cloud Platform Identity Authentication tile in hello Access Panel, you should get automatically signed-on tooyour SAP HANA Cloud Platform Identity Authentication application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0dea2-244">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="0dea2-244">Additional resources</span></span>

* [<span data-ttu-id="0dea2-245">Lista samouczków dotyczących tooIntegrate aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0dea2-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0dea2-246">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0dea2-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_06.png

[100]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-hana-cloud-platform-identity-authentication-tutorial/tutorial_general_203.png