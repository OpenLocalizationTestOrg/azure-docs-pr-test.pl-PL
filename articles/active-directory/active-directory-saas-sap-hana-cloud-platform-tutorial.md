---
title: 'Samouczek: Integracji Azure Active Directory z SAP HANA Cloud Platform | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak toouse SAP HANA Cloud Platform z usługą Azure Active Directory tooenable pojedynczy logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: bd398225-8bd8-4697-9a44-af6e6679113a
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: cc6610969b1c7b08f776e6969a5977fc75eb9ab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a><span data-ttu-id="ce3d8-103">Samouczek: integracja usługi Azure Active Directory z platformą w chmurze SAP HANA</span><span class="sxs-lookup"><span data-stu-id="ce3d8-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform</span></span>
<span data-ttu-id="ce3d8-104">Celem Hello tego samouczka jest tooshow integracji hello Azure i SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-104">hello objective of this tutorial is tooshow hello integration of Azure and SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="ce3d8-105">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ce3d8-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="ce3d8-106">Ważnej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ce3d8-106">A valid Azure subscription</span></span>
* <span data-ttu-id="ce3d8-107">Konta programu SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="ce3d8-107">A SAP HANA Cloud Platform account</span></span>

<span data-ttu-id="ce3d8-108">Ten samouczek hello użytkowników usługi Azure AD przypisano tooSAP HANA Cloud Platform będzie możliwe toosingle logowania do aplikacji hello przy użyciu hello [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ce3d8-108">After completing this tutorial, hello Azure AD users you have assigned tooSAP HANA Cloud Platform will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="ce3d8-109">Należy toodeploy własnej aplikacji lub subskrypcja tooan aplikacji na platformie chmury SAP HANA pojedynczego tootest konta logowania.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-109">You need toodeploy your own application or subscribe tooan application on your SAP HANA Cloud Platform account tootest single sign on.</span></span> <span data-ttu-id="ce3d8-110">W tym samouczku aplikacja jest wdrażana na koncie hello.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-110">In this tutorial, an application is deployed in hello account.</span></span>
> 
> 

<span data-ttu-id="ce3d8-111">Scenariusz Hello opisane w tym samouczku składa się z powitania po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="ce3d8-111">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="ce3d8-112">Włączanie integracji aplikacji hello SAP HANA chmury platformy</span><span class="sxs-lookup"><span data-stu-id="ce3d8-112">Enabling hello application integration for SAP HANA Cloud Platform</span></span>
2. <span data-ttu-id="ce3d8-113">Konfigurowanie rejestracji jednokrotnej (SSO)</span><span class="sxs-lookup"><span data-stu-id="ce3d8-113">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="ce3d8-114">Przypisanie roli użytkownika tooa</span><span class="sxs-lookup"><span data-stu-id="ce3d8-114">Assigning a role tooa user</span></span>
4. <span data-ttu-id="ce3d8-115">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="ce3d8-115">Assigning users</span></span>

<span data-ttu-id="ce3d8-116">![Scenariusz](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "scenariusza")</span><span class="sxs-lookup"><span data-stu-id="ce3d8-116">![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-sap-hana-cloud-platform"></a><span data-ttu-id="ce3d8-117">Włączanie integracji aplikacji hello SAP HANA chmury platformy</span><span class="sxs-lookup"><span data-stu-id="ce3d8-117">Enabling hello application integration for SAP HANA Cloud Platform</span></span>
<span data-ttu-id="ce3d8-118">Celem Hello w tej sekcji jest toooutline sposób integracji aplikacji hello tooenable platformy chmury SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-118">hello objective of this section is toooutline how tooenable hello application integration for SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="ce3d8-119">**Integracja aplikacji hello tooenable platformy SAP HANA chmury, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ce3d8-119">**tooenable hello application integration for SAP HANA Cloud Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce3d8-120">W hello portalu zarządzania Azure, w okienku nawigacji po lewej stronie powitania kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-120">In hello Azure Management Portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="ce3d8-121">![Usługi Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "usługi Active Directory")</span><span class="sxs-lookup"><span data-stu-id="ce3d8-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="ce3d8-122">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-122">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="ce3d8-123">Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-123">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="ce3d8-124">![Aplikacje](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "aplikacji")</span><span class="sxs-lookup"><span data-stu-id="ce3d8-124">![Applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="ce3d8-125">Kliknij przycisk **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-125">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="ce3d8-126">![Dodaj aplikację](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Dodaj aplikację")</span><span class="sxs-lookup"><span data-stu-id="ce3d8-126">![Add application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="ce3d8-127">Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-127">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="ce3d8-128">![Dodawanie aplikacji z gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "dodać aplikację z gallerry")</span><span class="sxs-lookup"><span data-stu-id="ce3d8-128">![Add an application from gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="ce3d8-129">W hello **pole wyszukiwania**, typ **SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-129">In hello **search box**, type **SAP HANA Cloud Platform**.</span></span>
   
    <span data-ttu-id="ce3d8-130">![Galerii aplikacji](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "galerii aplikacji")</span><span class="sxs-lookup"><span data-stu-id="ce3d8-130">![Application Gallery](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Application Gallery")</span></span>
7. <span data-ttu-id="ce3d8-131">Wybierz w okienku wyników hello **SAP HANA Cloud Platform**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-131">In hello results pane, select **SAP HANA Cloud Platform**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="ce3d8-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span><span class="sxs-lookup"><span data-stu-id="ce3d8-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="ce3d8-133">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ce3d8-133">Configure single sign-on</span></span>

<span data-ttu-id="ce3d8-134">Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooSAP HANA Cloud Platform do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-134">hello objective of this section is toooutline how tooenable users tooauthenticate tooSAP HANA Cloud Platform with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="ce3d8-135">W ramach tej procedury jest wymagana tooupload dzierżawcy SAP HANA Cloud Platform tooyour base-64 zakodowanego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-135">As part of this procedure, you are required tooupload a base-64 encoded certificate tooyour SAP HANA Cloud Platform tenant.</span></span>  

<span data-ttu-id="ce3d8-136">Jeśli nie masz doświadczenia z tej procedury, zobacz [jak tooconvert pliku binarnego certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="ce3d8-136">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="ce3d8-137">**tooconfigure logowanie jednokrotne, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ce3d8-137">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce3d8-138">W hello klasycznego portalu Azure na powitania **SAP HANA Cloud Platform** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować rejestrację jednokrotną**okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-138">In hello Azure classic portal, on hello **SAP HANA Cloud Platform** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="ce3d8-139">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="ce3d8-139">![Configure single sign-on](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="ce3d8-140">Na powitania **jak ma toosign użytkowników na tooSAP platformy w chmurze HANA** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-140">On hello **How would you like users toosign on tooSAP HANA Cloud Platform** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="ce3d8-141">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="ce3d8-141">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="ce3d8-142">W oknie przeglądarki sieci web inną logowania toohello SAP HANA Cloud Platform w Panelu sterowania na https://account. \<hosta pozioma\>.ondemand.com/cockpit (np.: *https://account.hanatrial.ondemand.com/cockpit*).</span><span class="sxs-lookup"><span data-stu-id="ce3d8-142">In a different web browser window, sign on toohello SAP HANA Cloud Platform Cockpit at https://account.\<landscape host\>.ondemand.com/cockpit (e.g.: *https://account.hanatrial.ondemand.com/cockpit*).</span></span>
4. <span data-ttu-id="ce3d8-143">Kliknij przycisk hello **zaufania** kartę.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-143">Click hello **Trust** tab.</span></span>
   
    <span data-ttu-id="ce3d8-144">![Zaufania](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "zaufania")</span><span class="sxs-lookup"><span data-stu-id="ce3d8-144">![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span></span>
5. <span data-ttu-id="ce3d8-145">W sekcji Zarządzanie zaufania należy wykonać hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="ce3d8-145">In trust management section, perform hello following steps:</span></span>
   
    <span data-ttu-id="ce3d8-146">![Pobranie metadanych](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "pobranie metadanych")</span><span class="sxs-lookup"><span data-stu-id="ce3d8-146">![Get Metadata](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Get Metadata")</span></span>
   
   1. <span data-ttu-id="ce3d8-147">Kliknij przycisk hello **lokalnego dostawcy usług** kartę.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-147">Click hello **Local Service Provider** tab.</span></span>
   2. <span data-ttu-id="ce3d8-148">toodownload hello SAP HANA Cloud Platform pliku metadanych, kliknij przycisk **pobrać metadanych**.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-148">toodownload hello SAP HANA Cloud Platform metadata file, click **Get Metadata**.</span></span>
6. <span data-ttu-id="ce3d8-149">W hello Azure Active klasycznego portalu na powitania **Konfigurowanie adresu URL aplikacji** , wykonaj następujące kroki hello, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-149">In hello Azure Active classic portal, on hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
    <span data-ttu-id="ce3d8-150">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="ce3d8-150">![Configure App URL](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configure App URL")</span></span>
   
   1. <span data-ttu-id="ce3d8-151">W hello **na adres URL logowania** pole tekstowe, wprowadź adres URL hello używany przez Twoje toosign użytkowników w Twojej **SAP HANA Cloud Platform** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-151">In hello **Sign On URL** textbox, type hello URL used by your users toosign into your **SAP HANA Cloud Platform** application.</span></span> <span data-ttu-id="ce3d8-152">To jest adres URL dotyczący konta hello zasobu chronionego w aplikacji platformy chmury SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-152">This is hello account-specific URL of a protected resource in your SAP HANA Cloud Platform application.</span></span> <span data-ttu-id="ce3d8-153">Witaj adres URL jest oparta na powitania następującego wzorca: *https://\<applicationName\>\<accountName\>.\< host pozioma\>.ondemand.com/\<ścieżki\_do\_chronione\_zasobów\>*  (np.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span><span class="sxs-lookup"><span data-stu-id="ce3d8-153">hello URL is based on hello following pattern: *https://\<applicationName\>\<accountName\>.\<landscape host\>.ondemand.com/\<path\_to\_protected\_resource\>* (e.g.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="ce3d8-154">To jest adres URL hello w aplikacji SAP HANA Cloud Platform, która wymaga hello tooauthenticate użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-154">This is hello URL in your SAP HANA Cloud Platform application that requires hello user tooauthenticate.</span></span>
     > 

   2. <span data-ttu-id="ce3d8-155">Otwórz plik metadanych platformy chmury SAP HANA hello pobrane, a następnie zlokalizuj hello **ns3:AssertionConsumerService** tagu.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-155">Open hello downloaded SAP HANA Cloud Platform metadata file, and then locate hello **ns3:AssertionConsumerService** tag.</span></span>
   3. <span data-ttu-id="ce3d8-156">Skopiuj wartość hello hello **lokalizacji** atrybutu, a następnie wklej go do hello **SAP HANA Cloud Platform adres URL odpowiedzi służący** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-156">Copy hello value of hello **Location** attribute, and then paste it into hello **SAP HANA Cloud Platform Reply URL** textbox.</span></span>

7. <span data-ttu-id="ce3d8-157">Na powitania **skonfigurować logowanie jednokrotne w SAP HANA Cloud Platform** strony, toodownload metadanych programu kliknij **pobierania metadanych**, a następnie zapisz plik hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-157">On hello **Configure single sign-on at SAP HANA Cloud Platform** page, toodownload your metadata, click **Download metadata**, and then save hello file on your computer.</span></span>
   
    <span data-ttu-id="ce3d8-158">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="ce3d8-158">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configure Single Sign-On")</span></span>
8. <span data-ttu-id="ce3d8-159">Na powitania SAP HANA Cloud Platform Panelu sterowania, w hello **lokalnego dostawcy usług** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ce3d8-159">On hello SAP HANA Cloud Platform Cockpit, in hello **Local Service Provider** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="ce3d8-160">![Zaufania zarządzania](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "zaufania zarządzania")</span><span class="sxs-lookup"><span data-stu-id="ce3d8-160">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")</span></span>
   
  1. <span data-ttu-id="ce3d8-161">Kliknij pozycję **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-161">Click **Edit**.</span></span>
  2. <span data-ttu-id="ce3d8-162">Jako **typu konfiguracji**, wybierz pozycję **niestandardowy**.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-162">As **Configuration Type**, select **Custom**.</span></span>
  3. <span data-ttu-id="ce3d8-163">Jako **lokalna nazwa dostawcy**, pozostaw wartość domyślną hello.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-163">As **Local Provider Name**, leave hello default value.</span></span>
  4. <span data-ttu-id="ce3d8-164">toogenerate **klucza podpisywania** i **certyfikat podpisywania** parę kluczy, kliknij przycisk **generowanie pary klucz**.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-164">toogenerate a **Signing Key** and a **Signing Certificate** key pair, click **Generate Key Pair**.</span></span>
  5. <span data-ttu-id="ce3d8-165">Jako **główna propagacji**, wybierz pozycję **wyłączone**.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-165">As **Principal Propagation**, select **Disabled**.</span></span>
  6. <span data-ttu-id="ce3d8-166">Jako **siły uwierzytelniania**, wybierz pozycję **wyłączone**.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-166">As **Force Authentication**, select **Disabled**.</span></span>
  7. <span data-ttu-id="ce3d8-167">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-167">Click **Save**.</span></span>

9. <span data-ttu-id="ce3d8-168">Kliknij przycisk hello **zaufany dostawca tożsamości** , a następnie kliknij pozycję **dodać zaufanego dostawcę tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-168">Click hello **Trusted Identity Provider** tab, and then click **Add Trusted Identity Provider**.</span></span>
   
    <span data-ttu-id="ce3d8-169">![Zaufania zarządzania](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "zaufania zarządzania")</span><span class="sxs-lookup"><span data-stu-id="ce3d8-169">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="ce3d8-170">toomanage hello listy zaufanych dostawców tożsamości, należy toohave wybrany hello niestandardowy typ konfiguracji w hello sekcji lokalnego dostawcy usług.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-170">toomanage hello list of trusted identity providers, you need toohave chosen hello Custom configuration type in hello Local Service Provider section.</span></span> <span data-ttu-id="ce3d8-171">Typ konfiguracji domyślnej masz toohello zaufania nie można edytować i niejawne SAP Identyfikatora usługi.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-171">For Default configuration type, you have a non-editable and implicit trust toohello SAP ID Service.</span></span> <span data-ttu-id="ce3d8-172">Dla żadnego nie masz żadnych ustawień zaufania.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-172">For None, you don't have any trust settings.</span></span>
    > 
    > 

10. <span data-ttu-id="ce3d8-173">Kliknij przycisk hello **ogólne** , a następnie kliknij pozycję **Przeglądaj** tooupload hello pobrany plik metadanych.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-173">Click hello **General** tab, and then click **Browse** tooupload hello downloaded metadata file.</span></span>
    
    <span data-ttu-id="ce3d8-174">![Zaufania zarządzania](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "zaufania zarządzania")</span><span class="sxs-lookup"><span data-stu-id="ce3d8-174">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="ce3d8-175">Po przekazaniu pliku metadanych hello, wartości hello **URL rejestracji jednokrotnej**, **pojedynczego adresu URL wylogowania** i **certyfikat podpisywania** są wypełniane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-175">After uploading hello metadata file, hello values for **Single Sign-on URL**, **Single Logout URL** and **Signing Certificate** are populated automatically.</span></span>
    > 
    > 

11. <span data-ttu-id="ce3d8-176">Kliknij przycisk hello **atrybuty** kartę.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-176">Click hello **Attributes** tab.</span></span>
12. <span data-ttu-id="ce3d8-177">Na powitania **atrybuty** karcie, wykonaj powitania po kroku:</span><span class="sxs-lookup"><span data-stu-id="ce3d8-177">On hello **Attributes** tab, perform hello following step:</span></span>
    
    <span data-ttu-id="ce3d8-178">![Atrybuty](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "atrybutów")</span><span class="sxs-lookup"><span data-stu-id="ce3d8-178">![Attributes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributes")</span></span> 
  * <span data-ttu-id="ce3d8-179">Kliknij przycisk **atrybutu Add Assertion-Based**, a następnie dodaj następujące atrybuty oparte na potwierdzenie hello:</span><span class="sxs-lookup"><span data-stu-id="ce3d8-179">Click **Add Assertion-Based Attribute**, and then add hello following assertion-based attributes:</span></span>
       
    | <span data-ttu-id="ce3d8-180">Atrybut potwierdzenia</span><span class="sxs-lookup"><span data-stu-id="ce3d8-180">Assertion Attribute</span></span> | <span data-ttu-id="ce3d8-181">Atrybut podmiotu</span><span class="sxs-lookup"><span data-stu-id="ce3d8-181">Principal Attribute</span></span> |
    | --- | --- |
    | <span data-ttu-id="ce3d8-182">http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/givenName</span><span class="sxs-lookup"><span data-stu-id="ce3d8-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span></span> |<span data-ttu-id="ce3d8-183">Imię</span><span class="sxs-lookup"><span data-stu-id="ce3d8-183">firstname</span></span> |
    | <span data-ttu-id="ce3d8-184">http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/surname</span><span class="sxs-lookup"><span data-stu-id="ce3d8-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span></span> |<span data-ttu-id="ce3d8-185">nazwisko</span><span class="sxs-lookup"><span data-stu-id="ce3d8-185">lastname</span></span> |
    | <span data-ttu-id="ce3d8-186">http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/emailaddress</span><span class="sxs-lookup"><span data-stu-id="ce3d8-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span></span> |<span data-ttu-id="ce3d8-187">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="ce3d8-187">email</span></span> 
   
     >[!NOTE]
     ><span data-ttu-id="ce3d8-188">Konfiguracja Hello atrybutów hello zależy od tego, jak aplikacji hello na HCP są tworzone, tj. atrybuty, które oczekiwanym hello odpowiedzi SAML i w których nazwa (atrybut podmiotu zabezpieczeń) będą uzyskiwać dostęp do tego atrybutu w kodzie hello.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-188">hello configuration of hello Attributes depends on how hello application(s) on HCP are developed, i.e. which attribute(s) they expect in hello SAML response and under which name (Principal Attribute) they access this attribute in hello code.</span></span>
     > 
     >  

    1.  <span data-ttu-id="ce3d8-189">Witaj **domyślny atrybut** w hello zrzut ekranu jest tylko do celów ilustracyjnych.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-189">hello **Default Attribute** in hello screenshot is just for illustration purposes.</span></span> <span data-ttu-id="ce3d8-190">Nie jest wymagane toomake hello scenariusz pracy.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-190">It is not required toomake hello scenario work.</span></span>   
    2.  <span data-ttu-id="ce3d8-191">Witaj nazwy i wartości dla **atrybut podmiotu zabezpieczeń** pokazano hello zrzut ekranu zależą od tego, jak aplikacja hello został utworzony.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-191">hello names and values for **Principal Attribute** shown in hello screenshot depend on how hello application is developed.</span></span> <span data-ttu-id="ce3d8-192">Istnieje możliwość, że aplikacja wymaga innego mapowania.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-192">It is possible that your application requires different mappings.</span></span>
     
13. <span data-ttu-id="ce3d8-193">W hello klasycznego portalu Azure na powitania **skonfigurować logowanie jednokrotne w SAP HANA Cloud Platform** dialogu strony, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete**.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-193">In hello Azure classic portal, on hello **Configure single sign-on at SAP HANA Cloud Platform** dialogue page, select hello single sign-on configuration confirmation, and then click **Complete**.</span></span>
    
    <span data-ttu-id="ce3d8-194">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="ce3d8-194">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configure Single Sign-On")</span></span>

###<a name="assertion-based-groups"></a><span data-ttu-id="ce3d8-195">Grupy oparte na potwierdzenie</span><span class="sxs-lookup"><span data-stu-id="ce3d8-195">Assertion-based groups</span></span>
<span data-ttu-id="ce3d8-196">Ten opcjonalny krok można skonfigurować grupy oparte na potwierdzenie dla usługi Azure Active Directory dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-196">As an optional step, you can configure assertion-based groups for your Azure Active Directory Identity Provider.</span></span>

<span data-ttu-id="ce3d8-197">Na platformie programu SAP HANA chmury przy użyciu grup umożliwia przypisanie toodynamically, jeden lub więcej użytkowników tooone lub więcej ról w aplikacjach platformy chmury SAP HANA określany przez wartości atrybutów w hello SAML 2.0 potwierdzenia.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-197">Using groups on SAP HANA Cloud Platform allows you toodynamically assign one or more users tooone or more roles in your SAP HANA Cloud Platform applications, determined by values of attributes in hello SAML 2.0 assertion.</span></span> 

<span data-ttu-id="ce3d8-198">Na przykład jeśli hello potwierdzenia zawiera atrybut hello "*kontraktu = tymczasowego*", wszystkie grupy dodano toohello toobe użytkowników może być"*tymczasowego*".</span><span class="sxs-lookup"><span data-stu-id="ce3d8-198">For example, if hello assertion contains hello attribute "*contract=temporary*", you may want all affected users toobe added toohello group "*TEMPORARY*".</span></span> <span data-ttu-id="ce3d8-199">grupy Hello "*tymczasowego*" może zawierać co najmniej jedną rolę z co najmniej jednej aplikacji wdrożonych na koncie platformy chmury SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-199">hello group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP HANA Cloud Platform account.</span></span>
 
<span data-ttu-id="ce3d8-200">Grupy oparte na potwierdzenie należy użyć toosimultaneously przypisać wielu użytkowników tooone lub więcej ról aplikacji na koncie platformy chmury SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-200">Use assertion-based groups when you want toosimultaneously assign many users tooone or more roles of applications in your SAP HANA Cloud Platform account.</span></span> <span data-ttu-id="ce3d8-201">Jeśli chcesz tooassign tylko jednego lub małej liczby użytkowników toospecific ról, zalecamy przypisywania do nich bezpośrednio w hello "**autoryzacje**" hello SAP HANA Cloud Platform w Panelu sterowania na karcie.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-201">If you want tooassign only a single or small number of users toospecific roles, we recommend assigning them directly in hello “**Authorizations**” tab of hello SAP HANA Cloud Platform cockpit.</span></span>

## <a name="assign-a-role-tooa-user"></a><span data-ttu-id="ce3d8-202">Przypisywanie roli użytkownika tooa</span><span class="sxs-lookup"><span data-stu-id="ce3d8-202">Assign a role tooa user</span></span>
<span data-ttu-id="ce3d8-203">W kolejności tooenable usługi Azure AD użytkownicy toolog do programu SAP HANA Cloud Platform należy przypisać role w hello toothem SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-203">In order tooenable Azure AD users toolog into SAP HANA Cloud Platform, you must assign roles in hello SAP HANA Cloud Platform toothem.</span></span>

<span data-ttu-id="ce3d8-204">**tooassign tooa roli użytkownika, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="ce3d8-204">**tooassign a role tooa user, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce3d8-205">Zaloguj się za tooyour **SAP HANA Cloud Platform** Panelu sterowania.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-205">Log in tooyour **SAP HANA Cloud Platform** cockpit.</span></span>
2. <span data-ttu-id="ce3d8-206">Wykonaj następujące hello:</span><span class="sxs-lookup"><span data-stu-id="ce3d8-206">Perform hello following:</span></span>
   
   <span data-ttu-id="ce3d8-207">![Autoryzacje](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "zezwolenia")</span><span class="sxs-lookup"><span data-stu-id="ce3d8-207">![Authorizations](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Authorizations")</span></span>
   
  1. <span data-ttu-id="ce3d8-208">Kliknij przycisk **autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-208">Click **Authorization**.</span></span>
  2. <span data-ttu-id="ce3d8-209">Kliknij przycisk hello **użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-209">Click hello **Users** tab.</span></span>
  3. <span data-ttu-id="ce3d8-210">W hello **użytkownika** pole tekstowe, typ hello adres e-mail użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-210">In hello **User** textbox, type hello user’s email address.</span></span>
  4. <span data-ttu-id="ce3d8-211">Kliknij przycisk **przypisać** tooassign hello użytkownika tooa roli.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-211">Click **Assign** tooassign hello user tooa role.</span></span>
  5. <span data-ttu-id="ce3d8-212">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-212">Click **Save**.</span></span>

## <a name="assign-users"></a><span data-ttu-id="ce3d8-213">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="ce3d8-213">Assign users</span></span>
<span data-ttu-id="ce3d8-214">tootest konfiguracji, należy toogrant hello Azure AD użytkownicy mają tooallow przy użyciu Twojej aplikacji tooit dostępu przez przypisywanie ich.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-214">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="ce3d8-215">**tooassign użytkowników tooSAP HANA platformy w chmurze, należy wykonać hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="ce3d8-215">**tooassign users tooSAP HANA Cloud Platform, perform hello following steps:**</span></span>

1. <span data-ttu-id="ce3d8-216">W hello klasycznego portalu Azure Utwórz konto testu.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-216">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="ce3d8-217">Na powitania **SAP HANA Cloud Platform** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-217">On hello **SAP HANA Cloud Platform** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="ce3d8-218">![Przypisywanie użytkowników](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "przypisywanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="ce3d8-218">![Assign Users](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assign Users")</span></span>
3. <span data-ttu-id="ce3d8-219">Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** tooconfirm przypisania.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-219">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="ce3d8-220">![Tak](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "tak")</span><span class="sxs-lookup"><span data-stu-id="ce3d8-220">![Yes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="ce3d8-221">Jeśli chcesz tootest ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ce3d8-221">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="ce3d8-222">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ce3d8-222">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

