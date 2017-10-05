---
title: 'Samouczek: Integracji Azure Active Directory z SAP HANA Cloud Platform | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak używać SAP HANA Cloud Platform z usługą Azure Active Directory w celu włączenia logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
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
ms.openlocfilehash: e03bc2410a8d57363c558f723b3bfd0e69b3f4c0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana-cloud-platform"></a><span data-ttu-id="8f3c5-103">Samouczek: integracja usługi Azure Active Directory z platformą w chmurze SAP HANA</span><span class="sxs-lookup"><span data-stu-id="8f3c5-103">Tutorial: Azure Active Directory integration with SAP HANA Cloud Platform</span></span>
<span data-ttu-id="8f3c5-104">Celem tego samouczka jest pokazanie integracji Azure i SAP HANA Cloud Platform.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-104">The objective of this tutorial is to show the integration of Azure and SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="8f3c5-105">Scenariusz opisany w tym samouczku założono, że już następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8f3c5-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="8f3c5-106">Ważnej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8f3c5-106">A valid Azure subscription</span></span>
* <span data-ttu-id="8f3c5-107">Konta programu SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="8f3c5-107">A SAP HANA Cloud Platform account</span></span>

<span data-ttu-id="8f3c5-108">Ten samouczek użytkowników usługi Azure AD, zostały przypisane do SAP HANA Cloud Platform będzie można funkcji logowania jednokrotnego do aplikacji przy użyciu [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8f3c5-108">After completing this tutorial, the Azure AD users you have assigned to SAP HANA Cloud Platform will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

>[!IMPORTANT]
><span data-ttu-id="8f3c5-109">Należy wdrożyć własną aplikację lub subskrybować aplikację na Twoim koncie SAP HANA Cloud Platform testowanie funkcji logowania jednokrotnego w.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-109">You need to deploy your own application or subscribe to an application on your SAP HANA Cloud Platform account to test single sign on.</span></span> <span data-ttu-id="8f3c5-110">W tym samouczku aplikacja jest wdrażana w ramach konta.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-110">In this tutorial, an application is deployed in the account.</span></span>
> 
> 

<span data-ttu-id="8f3c5-111">Scenariusz opisany w tym samouczku składa się z następujących bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="8f3c5-111">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="8f3c5-112">Włączanie integracji aplikacji dla programu SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="8f3c5-112">Enabling the application integration for SAP HANA Cloud Platform</span></span>
2. <span data-ttu-id="8f3c5-113">Konfigurowanie rejestracji jednokrotnej (SSO)</span><span class="sxs-lookup"><span data-stu-id="8f3c5-113">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="8f3c5-114">Przypisywanie użytkownikowi roli</span><span class="sxs-lookup"><span data-stu-id="8f3c5-114">Assigning a role to a user</span></span>
4. <span data-ttu-id="8f3c5-115">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="8f3c5-115">Assigning users</span></span>

<span data-ttu-id="8f3c5-116">![Scenariusz](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "scenariusza")</span><span class="sxs-lookup"><span data-stu-id="8f3c5-116">![Scenario](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790795.png "Scenario")</span></span>

## <a name="enabling-the-application-integration-for-sap-hana-cloud-platform"></a><span data-ttu-id="8f3c5-117">Włączanie integracji aplikacji dla programu SAP HANA Cloud Platform</span><span class="sxs-lookup"><span data-stu-id="8f3c5-117">Enabling the application integration for SAP HANA Cloud Platform</span></span>
<span data-ttu-id="8f3c5-118">Celem tej sekcji jest przedstawiają sposób włączania integracji aplikacji dla platformy chmury SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-118">The objective of this section is to outline how to enable the application integration for SAP HANA Cloud Platform.</span></span>

<span data-ttu-id="8f3c5-119">**Aby włączyć integrację aplikacji dla programu SAP HANA Cloud Platform, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8f3c5-119">**To enable the application integration for SAP HANA Cloud Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="8f3c5-120">W portalu zarządzania Azure, w okienku nawigacji po lewej stronie kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-120">In the Azure Management Portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="8f3c5-121">![Usługi Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "usługi Active Directory")</span><span class="sxs-lookup"><span data-stu-id="8f3c5-121">![Active Directory](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="8f3c5-122">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-122">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="8f3c5-123">Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-123">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="8f3c5-124">![Aplikacje](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "aplikacji")</span><span class="sxs-lookup"><span data-stu-id="8f3c5-124">![Applications](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="8f3c5-125">Kliknij przycisk **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-125">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="8f3c5-126">![Dodaj aplikację](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Dodaj aplikację")</span><span class="sxs-lookup"><span data-stu-id="8f3c5-126">![Add application](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="8f3c5-127">Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-127">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="8f3c5-128">![Dodawanie aplikacji z gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "dodać aplikację z gallerry")</span><span class="sxs-lookup"><span data-stu-id="8f3c5-128">![Add an application from gallerry](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="8f3c5-129">W **pole wyszukiwania**, typ **SAP HANA Cloud Platform**.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-129">In the **search box**, type **SAP HANA Cloud Platform**.</span></span>
   
    <span data-ttu-id="8f3c5-130">![Galerii aplikacji](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "galerii aplikacji")</span><span class="sxs-lookup"><span data-stu-id="8f3c5-130">![Application Gallery](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790796.png "Application Gallery")</span></span>
7. <span data-ttu-id="8f3c5-131">W okienku wyników wybierz **SAP HANA Cloud Platform**, a następnie kliknij przycisk **Complete** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-131">In the results pane, select **SAP HANA Cloud Platform**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="8f3c5-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span><span class="sxs-lookup"><span data-stu-id="8f3c5-132">![SAP Hana](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793929.png "SAP Hana")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="8f3c5-133">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8f3c5-133">Configure single sign-on</span></span>

<span data-ttu-id="8f3c5-134">Celem tej sekcji jest przedstawiają sposób umożliwić użytkownikom uwierzytelnianie platformy Chmurowej SAP HANA do swojego konta w usłudze Azure AD przy użyciu federacyjnego na podstawie protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-134">The objective of this section is to outline how to enable users to authenticate to SAP HANA Cloud Platform with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="8f3c5-135">W ramach tej procedury jest wymagane do przekazania zakodowanego certyfikatu base-64 w dzierżawie platformy chmury SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-135">As part of this procedure, you are required to upload a base-64 encoded certificate to your SAP HANA Cloud Platform tenant.</span></span>  

<span data-ttu-id="8f3c5-136">Jeśli nie masz doświadczenia z tej procedury, zobacz [sposób konwertowania binarne certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="8f3c5-136">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="8f3c5-137">**Aby skonfigurować rejestrację jednokrotną, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8f3c5-137">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="8f3c5-138">W klasycznym portalu Azure na **SAP HANA Cloud Platform** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-138">In the Azure classic portal, on the **SAP HANA Cloud Platform** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="8f3c5-139">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="8f3c5-139">![Configure single sign-on](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC778552.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="8f3c5-140">Na **jak chcesz użytkownikom zalogować się do programu SAP HANA Cloud Platform** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-140">On the **How would you like users to sign on to SAP HANA Cloud Platform** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="8f3c5-141">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="8f3c5-141">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790797.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="8f3c5-142">W oknie przeglądarki innej witryny sieci web Zaloguj się do panelu sterowania SAP HANA Cloud Platform w https://account. \<hosta pozioma\>.ondemand.com/cockpit (np.: *https://account.hanatrial.ondemand.com/cockpit*).</span><span class="sxs-lookup"><span data-stu-id="8f3c5-142">In a different web browser window, sign on to the SAP HANA Cloud Platform Cockpit at https://account.\<landscape host\>.ondemand.com/cockpit (e.g.: *https://account.hanatrial.ondemand.com/cockpit*).</span></span>
4. <span data-ttu-id="8f3c5-143">Kliknij przycisk **zaufania** kartę.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-143">Click the **Trust** tab.</span></span>
   
    <span data-ttu-id="8f3c5-144">![Zaufania](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "zaufania")</span><span class="sxs-lookup"><span data-stu-id="8f3c5-144">![Trust](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790800.png "Trust")</span></span>
5. <span data-ttu-id="8f3c5-145">W sekcji Zarządzanie zaufania wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8f3c5-145">In trust management section, perform the following steps:</span></span>
   
    <span data-ttu-id="8f3c5-146">![Pobranie metadanych](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "pobranie metadanych")</span><span class="sxs-lookup"><span data-stu-id="8f3c5-146">![Get Metadata](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793930.png "Get Metadata")</span></span>
   
   1. <span data-ttu-id="8f3c5-147">Kliknij przycisk **lokalnego dostawcy usług** kartę.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-147">Click the **Local Service Provider** tab.</span></span>
   2. <span data-ttu-id="8f3c5-148">Aby pobrać pliku metadanych SAP HANA Cloud Platform, kliknij przycisk **pobrać metadanych**.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-148">To download the SAP HANA Cloud Platform metadata file, click **Get Metadata**.</span></span>
6. <span data-ttu-id="8f3c5-149">W portalu klasycznym Azure Active na **Konfigurowanie adresu URL aplikacji** , wykonaj następujące czynności, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-149">In the Azure Active classic portal, on the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
    <span data-ttu-id="8f3c5-150">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="8f3c5-150">![Configure App URL](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790798.png "Configure App URL")</span></span>
   
   1. <span data-ttu-id="8f3c5-151">W **na adres URL logowania** tekstowym, wpisz adres URL używany przez użytkowników do logowania się do sieci **SAP HANA Cloud Platform** aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-151">In the **Sign On URL** textbox, type the URL used by your users to sign into your **SAP HANA Cloud Platform** application.</span></span> <span data-ttu-id="8f3c5-152">To jest adres URL konta określonego zasobu chronionego w aplikacji platformy chmury SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-152">This is the account-specific URL of a protected resource in your SAP HANA Cloud Platform application.</span></span> <span data-ttu-id="8f3c5-153">Adres URL jest oparta na następujący wzór: *https://\<applicationName\>\<accountName\>.\< host pozioma\>.ondemand.com/\<ścieżki\_do\_chronione\_zasobów\>*  (np.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span><span class="sxs-lookup"><span data-stu-id="8f3c5-153">The URL is based on the following pattern: *https://\<applicationName\>\<accountName\>.\<landscape host\>.ondemand.com/\<path\_to\_protected\_resource\>* (e.g.: *https://xleavep1941203872trial.hanatrial.ondemand.com/xleave*)</span></span>
      
     >[!NOTE]
     ><span data-ttu-id="8f3c5-154">To jest adres URL w aplikacji SAP HANA Cloud Platform, która wymaga uwierzytelnienia użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-154">This is the URL in your SAP HANA Cloud Platform application that requires the user to authenticate.</span></span>
     > 

   2. <span data-ttu-id="8f3c5-155">Otwórz pobrany plik metadanych SAP HANA Cloud Platform, a następnie zlokalizuj **ns3:AssertionConsumerService** tagu.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-155">Open the downloaded SAP HANA Cloud Platform metadata file, and then locate the **ns3:AssertionConsumerService** tag.</span></span>
   3. <span data-ttu-id="8f3c5-156">Skopiuj wartość **lokalizacji** atrybutu, a następnie wklej go do **SAP HANA Cloud Platform adres URL odpowiedzi służący** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-156">Copy the value of the **Location** attribute, and then paste it into the **SAP HANA Cloud Platform Reply URL** textbox.</span></span>

7. <span data-ttu-id="8f3c5-157">Na **skonfigurować logowanie jednokrotne w SAP HANA Cloud Platform** , aby pobrać metadane, kliknij przycisk **pobierania metadanych**, a następnie zapisz plik na komputerze.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-157">On the **Configure single sign-on at SAP HANA Cloud Platform** page, to download your metadata, click **Download metadata**, and then save the file on your computer.</span></span>
   
    <span data-ttu-id="8f3c5-158">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="8f3c5-158">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790799.png "Configure Single Sign-On")</span></span>
8. <span data-ttu-id="8f3c5-159">Na SAP HANA Cloud Platform Panelu sterowania w **lokalnego dostawcy usług** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8f3c5-159">On the SAP HANA Cloud Platform Cockpit, in the **Local Service Provider** section, perform the following steps:</span></span>
   
    <span data-ttu-id="8f3c5-160">![Zaufania zarządzania](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "zaufania zarządzania")</span><span class="sxs-lookup"><span data-stu-id="8f3c5-160">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793931.png "Trust Management")</span></span>
   
  1. <span data-ttu-id="8f3c5-161">Kliknij pozycję **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-161">Click **Edit**.</span></span>
  2. <span data-ttu-id="8f3c5-162">Jako **typu konfiguracji**, wybierz pozycję **niestandardowy**.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-162">As **Configuration Type**, select **Custom**.</span></span>
  3. <span data-ttu-id="8f3c5-163">Jako **lokalna nazwa dostawcy**, pozostaw wartość domyślną.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-163">As **Local Provider Name**, leave the default value.</span></span>
  4. <span data-ttu-id="8f3c5-164">Aby wygenerować **klucza podpisywania** i **certyfikat podpisywania** parę kluczy, kliknij przycisk **generowanie pary klucz**.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-164">To generate a **Signing Key** and a **Signing Certificate** key pair, click **Generate Key Pair**.</span></span>
  5. <span data-ttu-id="8f3c5-165">Jako **główna propagacji**, wybierz pozycję **wyłączone**.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-165">As **Principal Propagation**, select **Disabled**.</span></span>
  6. <span data-ttu-id="8f3c5-166">Jako **siły uwierzytelniania**, wybierz pozycję **wyłączone**.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-166">As **Force Authentication**, select **Disabled**.</span></span>
  7. <span data-ttu-id="8f3c5-167">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-167">Click **Save**.</span></span>

9. <span data-ttu-id="8f3c5-168">Kliknij przycisk **zaufany dostawca tożsamości** , a następnie kliknij pozycję **dodać zaufanego dostawcę tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-168">Click the **Trusted Identity Provider** tab, and then click **Add Trusted Identity Provider**.</span></span>
   
    <span data-ttu-id="8f3c5-169">![Zaufania zarządzania](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "zaufania zarządzania")</span><span class="sxs-lookup"><span data-stu-id="8f3c5-169">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790802.png "Trust Management")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="8f3c5-170">Do zarządzania listą zaufanych dostawców tożsamości, musisz wybrany typ konfiguracji niestandardowej w sekcji lokalnego dostawcy usług.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-170">To manage the list of trusted identity providers, you need to have chosen the Custom configuration type in the Local Service Provider section.</span></span> <span data-ttu-id="8f3c5-171">Typ konfiguracji domyślnej masz nieedytowalnego i niejawne zaufania z usługą identyfikator SAP.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-171">For Default configuration type, you have a non-editable and implicit trust to the SAP ID Service.</span></span> <span data-ttu-id="8f3c5-172">Dla żadnego nie masz żadnych ustawień zaufania.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-172">For None, you don't have any trust settings.</span></span>
    > 
    > 

10. <span data-ttu-id="8f3c5-173">Kliknij przycisk **ogólne** , a następnie kliknij pozycję **Przeglądaj** można przekazać pliku pobranego metadanych.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-173">Click the **General** tab, and then click **Browse** to upload the downloaded metadata file.</span></span>
    
    <span data-ttu-id="8f3c5-174">![Zaufania zarządzania](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "zaufania zarządzania")</span><span class="sxs-lookup"><span data-stu-id="8f3c5-174">![Trust Management](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC793932.png "Trust Management")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="8f3c5-175">Po przekazaniu pliku metadanych wartości **URL rejestracji jednokrotnej**, **pojedynczego adresu URL wylogowania** i **certyfikat podpisywania** są wypełniane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-175">After uploading the metadata file, the values for **Single Sign-on URL**, **Single Logout URL** and **Signing Certificate** are populated automatically.</span></span>
    > 
    > 

11. <span data-ttu-id="8f3c5-176">Kliknij kartę **Atrybuty**.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-176">Click the **Attributes** tab.</span></span>
12. <span data-ttu-id="8f3c5-177">Na **atrybuty** karcie, wykonaj następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8f3c5-177">On the **Attributes** tab, perform the following step:</span></span>
    
    <span data-ttu-id="8f3c5-178">![Atrybuty](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "atrybutów")</span><span class="sxs-lookup"><span data-stu-id="8f3c5-178">![Attributes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790804.png "Attributes")</span></span> 
  * <span data-ttu-id="8f3c5-179">Kliknij przycisk **atrybutu Add Assertion-Based**, a następnie dodaj następujące atrybuty oparte na potwierdzenia:</span><span class="sxs-lookup"><span data-stu-id="8f3c5-179">Click **Add Assertion-Based Attribute**, and then add the following assertion-based attributes:</span></span>
       
    | <span data-ttu-id="8f3c5-180">Atrybut potwierdzenia</span><span class="sxs-lookup"><span data-stu-id="8f3c5-180">Assertion Attribute</span></span> | <span data-ttu-id="8f3c5-181">Atrybut podmiotu</span><span class="sxs-lookup"><span data-stu-id="8f3c5-181">Principal Attribute</span></span> |
    | --- | --- |
    | <span data-ttu-id="8f3c5-182">http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/givenName</span><span class="sxs-lookup"><span data-stu-id="8f3c5-182">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname</span></span> |<span data-ttu-id="8f3c5-183">Imię</span><span class="sxs-lookup"><span data-stu-id="8f3c5-183">firstname</span></span> |
    | <span data-ttu-id="8f3c5-184">http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/surname</span><span class="sxs-lookup"><span data-stu-id="8f3c5-184">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname</span></span> |<span data-ttu-id="8f3c5-185">nazwisko</span><span class="sxs-lookup"><span data-stu-id="8f3c5-185">lastname</span></span> |
    | <span data-ttu-id="8f3c5-186">http://schemas.xmlsoap.org/ws/2005/05/Identity/Claims/emailaddress</span><span class="sxs-lookup"><span data-stu-id="8f3c5-186">http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress</span></span> |<span data-ttu-id="8f3c5-187">Adres e-mail</span><span class="sxs-lookup"><span data-stu-id="8f3c5-187">email</span></span> 
   
     >[!NOTE]
     ><span data-ttu-id="8f3c5-188">Konfiguracja atrybutów, zależy od tego, jak aplikacje na HCP są tworzone, tj. atrybuty, które oczekiwane w odpowiedzi SAML i w których nazwa (atrybut podmiotu zabezpieczeń) będą uzyskiwać dostęp do tego atrybutu w kodzie.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-188">The configuration of the Attributes depends on how the application(s) on HCP are developed, i.e. which attribute(s) they expect in the SAML response and under which name (Principal Attribute) they access this attribute in the code.</span></span>
     > 
     >  

    1.  <span data-ttu-id="8f3c5-189">**Domyślny atrybut** na zrzucie ekranu jest tylko do celów ilustracyjnych.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-189">The **Default Attribute** in the screenshot is just for illustration purposes.</span></span> <span data-ttu-id="8f3c5-190">Nie jest wymagane dokonanie scenariuszu działać.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-190">It is not required to make the scenario work.</span></span>   
    2.  <span data-ttu-id="8f3c5-191">Nazwy i wartości dla **atrybut podmiotu zabezpieczeń** na zrzucie ekranu pokazano zależą od sposobu zaprojektowano w aplikacji.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-191">The names and values for **Principal Attribute** shown in the screenshot depend on how the application is developed.</span></span> <span data-ttu-id="8f3c5-192">Istnieje możliwość, że aplikacja wymaga innego mapowania.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-192">It is possible that your application requires different mappings.</span></span>
     
13. <span data-ttu-id="8f3c5-193">W klasycznym portalu Azure na **skonfigurować logowanie jednokrotne w SAP HANA Cloud Platform** dialogu strony, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij **Complete**.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-193">In the Azure classic portal, on the **Configure single sign-on at SAP HANA Cloud Platform** dialogue page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
    
    <span data-ttu-id="8f3c5-194">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="8f3c5-194">![Configure Single Sign-On](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC796933.png "Configure Single Sign-On")</span></span>

###<a name="assertion-based-groups"></a><span data-ttu-id="8f3c5-195">Grupy oparte na potwierdzenie</span><span class="sxs-lookup"><span data-stu-id="8f3c5-195">Assertion-based groups</span></span>
<span data-ttu-id="8f3c5-196">Ten opcjonalny krok można skonfigurować grupy oparte na potwierdzenie dla usługi Azure Active Directory dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-196">As an optional step, you can configure assertion-based groups for your Azure Active Directory Identity Provider.</span></span>

<span data-ttu-id="8f3c5-197">Na platformie programu SAP HANA chmury przy użyciu grup umożliwia dynamiczne przypisywanie co najmniej jednego użytkownika do co najmniej jedną rolę w aplikacjach platformy chmury SAP HANA określany przez wartości atrybutów w potwierdzenia SAML 2.0.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-197">Using groups on SAP HANA Cloud Platform allows you to dynamically assign one or more users to one or more roles in your SAP HANA Cloud Platform applications, determined by values of attributes in the SAML 2.0 assertion.</span></span> 

<span data-ttu-id="8f3c5-198">Na przykład, jeśli potwierdzenie zawiera atrybut "*kontraktu = tymczasowego*", może być wszystkich użytkowników mają zostać dodane do grupy"*tymczasowego*".</span><span class="sxs-lookup"><span data-stu-id="8f3c5-198">For example, if the assertion contains the attribute "*contract=temporary*", you may want all affected users to be added to the group "*TEMPORARY*".</span></span> <span data-ttu-id="8f3c5-199">Grupa "*tymczasowego*" może zawierać co najmniej jedną rolę z co najmniej jednej aplikacji wdrożonych na koncie platformy chmury SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-199">The group "*TEMPORARY*" may contain one or more roles from one or more applications deployed in your SAP HANA Cloud Platform account.</span></span>
 
<span data-ttu-id="8f3c5-200">Grupy oparte na potwierdzenie należy użyć jednocześnie przypisać wielu użytkowników do co najmniej jedną rolę aplikacji na koncie platformy chmury SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-200">Use assertion-based groups when you want to simultaneously assign many users to one or more roles of applications in your SAP HANA Cloud Platform account.</span></span> <span data-ttu-id="8f3c5-201">Jeśli chcesz przypisać tylko jednego lub mała liczba użytkowników do określonych ról, zalecane jest przypisywania do nich bezpośrednio w programie "**autoryzacje**" kartę SAP HANA Cloud Platform Panelu sterowania.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-201">If you want to assign only a single or small number of users to specific roles, we recommend assigning them directly in the “**Authorizations**” tab of the SAP HANA Cloud Platform cockpit.</span></span>

## <a name="assign-a-role-to-a-user"></a><span data-ttu-id="8f3c5-202">Przypisywanie użytkownikowi roli</span><span class="sxs-lookup"><span data-stu-id="8f3c5-202">Assign a role to a user</span></span>
<span data-ttu-id="8f3c5-203">Aby włączyć użytkowników usługi Azure AD zalogować się do programu SAP HANA Cloud Platform, należy przypisać do nich ról na platformie programu SAP HANA chmury.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-203">In order to enable Azure AD users to log into SAP HANA Cloud Platform, you must assign roles in the SAP HANA Cloud Platform to them.</span></span>

<span data-ttu-id="8f3c5-204">**Aby przypisać rolę do użytkownika, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8f3c5-204">**To assign a role to a user, perform the following steps:**</span></span>

1. <span data-ttu-id="8f3c5-205">Zaloguj się do Twojego **SAP HANA Cloud Platform** Panelu sterowania.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-205">Log in to your **SAP HANA Cloud Platform** cockpit.</span></span>
2. <span data-ttu-id="8f3c5-206">Wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="8f3c5-206">Perform the following:</span></span>
   
   <span data-ttu-id="8f3c5-207">![Autoryzacje](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "zezwolenia")</span><span class="sxs-lookup"><span data-stu-id="8f3c5-207">![Authorizations](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790805.png "Authorizations")</span></span>
   
  1. <span data-ttu-id="8f3c5-208">Kliknij przycisk **autoryzacji**.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-208">Click **Authorization**.</span></span>
  2. <span data-ttu-id="8f3c5-209">Kliknij przycisk **użytkowników** kartę.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-209">Click the **Users** tab.</span></span>
  3. <span data-ttu-id="8f3c5-210">W **użytkownika** tekstowym, wpisz adres e-mail użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-210">In the **User** textbox, type the user’s email address.</span></span>
  4. <span data-ttu-id="8f3c5-211">Kliknij przycisk **przypisać** można przypisać do roli użytkownika.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-211">Click **Assign** to assign the user to a role.</span></span>
  5. <span data-ttu-id="8f3c5-212">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-212">Click **Save**.</span></span>

## <a name="assign-users"></a><span data-ttu-id="8f3c5-213">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="8f3c5-213">Assign users</span></span>
<span data-ttu-id="8f3c5-214">Aby przetestować konfigurację, musisz przyznać użytkowników usługi Azure AD, czy chcesz zezwolić, używając przypisywania do nich dostęp aplikacji do niego.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-214">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="8f3c5-215">**Do przypisywania użytkowników do programu SAP HANA Cloud Platform, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="8f3c5-215">**To assign users to SAP HANA Cloud Platform, perform the following steps:**</span></span>

1. <span data-ttu-id="8f3c5-216">W klasycznym portalu Azure Utwórz konto testu.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-216">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="8f3c5-217">Na **SAP HANA Cloud Platform** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-217">On the **SAP HANA Cloud Platform** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="8f3c5-218">![Przypisywanie użytkowników](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "przypisywanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="8f3c5-218">![Assign Users](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC790806.png "Assign Users")</span></span>
3. <span data-ttu-id="8f3c5-219">Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** o potwierdzenie przypisania.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-219">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="8f3c5-220">![Tak](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "tak")</span><span class="sxs-lookup"><span data-stu-id="8f3c5-220">![Yes](./media/active-directory-saas-sap-hana-cloud-platform-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="8f3c5-221">Jeśli chcesz przetestować ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="8f3c5-221">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="8f3c5-222">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8f3c5-222">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

