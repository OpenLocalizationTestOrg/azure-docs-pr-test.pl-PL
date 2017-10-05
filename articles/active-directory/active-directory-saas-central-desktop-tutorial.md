---
title: "Samouczek: Integracji Azure Active Directory przy użyciu centralnej pulpitu | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak włączyć logowanie jednokrotne, automatyczne Inicjowanie obsługi i inne za pomocą centralnej pulpitu z usługą Azure Active Directory!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: fe32c1d68040ceb9d9de2ad6c4a6dc9ea93f5aef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a><span data-ttu-id="336a7-103">Samouczek: Integracji Azure Active Directory przy użyciu centralnej pulpitu</span><span class="sxs-lookup"><span data-stu-id="336a7-103">Tutorial: Azure Active Directory integration with Central Desktop</span></span>
<span data-ttu-id="336a7-104">Celem tego samouczka jest pokazanie integracji Azure i pulpitu centralnej.</span><span class="sxs-lookup"><span data-stu-id="336a7-104">The objective of this tutorial is to show the integration of Azure and Central Desktop.</span></span> <span data-ttu-id="336a7-105">Scenariusz opisany w tym samouczku założono, że już następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="336a7-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="336a7-106">Ważnej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="336a7-106">A valid Azure subscription</span></span>
* <span data-ttu-id="336a7-107">Centralna pulpitu jednokrotne włączone subskrypcji / dzierżawy centralnej pulpitu</span><span class="sxs-lookup"><span data-stu-id="336a7-107">A Central desktop single sign on enabled subscription / Central desktop tenant</span></span>

<span data-ttu-id="336a7-108">Scenariusz opisany w tym samouczku składa się z następujących bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="336a7-108">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="336a7-109">Włączanie integracji aplikacji dla komputerów typu Desktop centralnej</span><span class="sxs-lookup"><span data-stu-id="336a7-109">Enabling the application integration for Central Desktop</span></span>
* <span data-ttu-id="336a7-110">Konfigurowanie rejestracji jednokrotnej (SSO)</span><span class="sxs-lookup"><span data-stu-id="336a7-110">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="336a7-111">Konfigurowanie Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="336a7-111">Configuring user provisioning</span></span>
* <span data-ttu-id="336a7-112">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="336a7-112">Assigning users</span></span>

<span data-ttu-id="336a7-113">![Scenariusz](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "scenariusza")</span><span class="sxs-lookup"><span data-stu-id="336a7-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-central-desktop"></a><span data-ttu-id="336a7-114">Włącz integrację aplikacji dla komputerów typu Desktop centralnej</span><span class="sxs-lookup"><span data-stu-id="336a7-114">Enable the application integration for Central Desktop</span></span>
<span data-ttu-id="336a7-115">Celem tej sekcji jest przedstawiają sposób włączania integracji aplikacji dla komputerów typu Desktop centralnej.</span><span class="sxs-lookup"><span data-stu-id="336a7-115">The objective of this section is to outline how to enable the application integration for Central Desktop.</span></span>

<span data-ttu-id="336a7-116">**Aby włączyć integrację aplikacji dla komputerów typu Desktop centralnej, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="336a7-116">**To enable the application integration for Central Desktop, perform the following steps:**</span></span>

1. <span data-ttu-id="336a7-117">W klasycznym portalu Azure, w okienku nawigacji po lewej stronie kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="336a7-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="336a7-118">![Usługi Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "usługi Active Directory")</span><span class="sxs-lookup"><span data-stu-id="336a7-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="336a7-119">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="336a7-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="336a7-120">Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="336a7-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="336a7-121">![Aplikacje](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "aplikacji")</span><span class="sxs-lookup"><span data-stu-id="336a7-121">![Applications](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="336a7-122">Kliknij przycisk **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="336a7-122">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="336a7-123">![Dodaj aplikację](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Dodaj aplikację")</span><span class="sxs-lookup"><span data-stu-id="336a7-123">![Add application](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="336a7-124">Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.</span><span class="sxs-lookup"><span data-stu-id="336a7-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="336a7-125">![Dodawanie aplikacji z gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "dodać aplikację z gallerry")</span><span class="sxs-lookup"><span data-stu-id="336a7-125">![Add an application from gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="336a7-126">W **pole wyszukiwania**, typ **centralnej pulpitu**.</span><span class="sxs-lookup"><span data-stu-id="336a7-126">In the **search box**, type **Central Desktop**.</span></span>
   
   <span data-ttu-id="336a7-127">![Galerii aplikacji](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "galerii aplikacji")</span><span class="sxs-lookup"><span data-stu-id="336a7-127">![Application gallery](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Application gallery")</span></span>
7. <span data-ttu-id="336a7-128">W okienku wyników wybierz **centralnej pulpitu**, a następnie kliknij przycisk **Complete** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="336a7-128">In the results pane, select **Central Desktop**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="336a7-129">![Centralna pulpitu](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "centralnej pulpitu")</span><span class="sxs-lookup"><span data-stu-id="336a7-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="336a7-130">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="336a7-130">Configure single sign-on</span></span>

<span data-ttu-id="336a7-131">Celem tej sekcji jest przedstawiają sposób umożliwić użytkownikom uwierzytelnianie na pulpicie centralnej do swojego konta w usłudze Azure AD przy użyciu federacyjnego na podstawie protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="336a7-131">The objective of this section is to outline how to enable users to authenticate to Central Desktop with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="336a7-132">W ramach tej procedury jest wymagane do przekazania do dzierżawy centralnej pulpitu zakodowanego certyfikatu base-64.</span><span class="sxs-lookup"><span data-stu-id="336a7-132">As part of this procedure, you are required to upload a base-64 encoded certificate to your Central Desktop tenant.</span></span>  
<span data-ttu-id="336a7-133">Jeśli nie masz doświadczenia z tej procedury, zobacz [sposób konwertowania binarne certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="336a7-133">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="336a7-134">**Aby skonfigurować rejestrację jednokrotną, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="336a7-134">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="336a7-135">W klasycznym portalu Azure na **centralnej pulpitu** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć ** skonfigurować rejestrację jednokrotną ** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="336a7-135">In the Azure classic portal, on the **Central Desktop** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
   <span data-ttu-id="336a7-136">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="336a7-136">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="336a7-137">Na **jak chcesz użytkownikom zalogować się na pulpicie centralnej** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="336a7-137">On the **How would you like users to sign on to Central Desktop** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="336a7-138">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="336a7-138">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="336a7-139">Na **Konfigurowanie adresu URL aplikacji** , wykonaj następujące czynności, a następnie kliknij przycisk **dalej**:</span><span class="sxs-lookup"><span data-stu-id="336a7-139">On the **Configure App URL** page, perform the following steps, and then click **Next**:</span></span> 
   
   1. <span data-ttu-id="336a7-140">W **centralnej pulpitu adres URL logowania** tekstowym, wpisz adres URL dzierżawy centralnej pulpitu (np.: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="336a7-140">In the **Central Desktop Sign In URL** textbox, type the URL of your Central Desktop tenant (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   2. <span data-ttu-id="336a7-141">W polu tekstowym adres URL odpowiedzi Central pulpitu, wpisz adres URL centralnej AssertionConsumerService pulpitu (np.: https://contoso.centraldesktop.com/saml2-assertion.php).</span><span class="sxs-lookup"><span data-stu-id="336a7-141">In the Central  Desktop Reply URL textbox, type your Central Desktop AssertionConsumerService URL (e.g.:  https://contoso.centraldesktop.com/saml2-assertion.php).</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="336a7-142">Można pobrać wartości z centralnego pulpitu metadanych (np.: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="336a7-142">You can get the value from the central desktop metadata (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   >  
   
   <span data-ttu-id="336a7-143">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="336a7-143">![Configure app URL](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configure app URL")</span></span>
4. <span data-ttu-id="336a7-144">Na **skonfigurować logowanie jednokrotne w centralnej pulpitu** , aby pobrać certyfikat, kliknij przycisk **pobierania certyfikatu**, a następnie zapisz plik certyfikatu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="336a7-144">On the **Configure single sign-on at Central Desktop** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
  <span data-ttu-id="336a7-145">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="336a7-145">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="336a7-146">Zaloguj się do Twojego **centralnej pulpitu** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="336a7-146">Log in to your **Central Desktop** tenant.</span></span>
6. <span data-ttu-id="336a7-147">Przejdź do **ustawienia**, kliknij przycisk **zaawansowane**, a następnie kliknij przycisk **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="336a7-147">Go to **Settings**, click **Advanced**, and then click **Single Sign On**.</span></span>
   
  <span data-ttu-id="336a7-148">![Instalator — zaawansowane](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Instalator — zaawansowane")</span><span class="sxs-lookup"><span data-stu-id="336a7-148">![Setup - Advanced](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span></span>
7. <span data-ttu-id="336a7-149">Na **pojedynczy znak na ustawienia** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="336a7-149">On the **Single Sign On Settings** page, perform the following steps:</span></span>
   
  <span data-ttu-id="336a7-150">![Rejestracja jednokrotna ustawień](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Rejestracja jednokrotna ustawień")</span><span class="sxs-lookup"><span data-stu-id="336a7-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span></span>
   
  1. <span data-ttu-id="336a7-151">Wybierz **Włącz SAML v2 logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="336a7-151">Select **Enable SAML v2 Single Sign On**.</span></span>
  2. <span data-ttu-id="336a7-152">W klasycznym portalu Azure na **skonfigurować logowanie jednokrotne w centralnej pulpitu** strony, skopiuj **adres URL wystawcy** wartość, a następnie wklej ją do **adres URL logowania jednokrotnego** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="336a7-152">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Issuer URL** value, and then paste it into the **SSO URL** textbox.</span></span>
  3. <span data-ttu-id="336a7-153">W klasycznym portalu Azure na **skonfigurować logowanie jednokrotne w centralnej pulpitu** strony, skopiuj **zdalnego adresu URL logowania** wartość, a następnie wklej ją do **adres URL logowania jednokrotnego logowania** pole tekstowe .</span><span class="sxs-lookup"><span data-stu-id="336a7-153">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Remote Login URL** value, and then paste it into the **SSO Login URL** textbox.</span></span>
  4. <span data-ttu-id="336a7-154">W klasycznym portalu Azure na **skonfigurować logowanie jednokrotne w centralnej pulpitu** strony, skopiuj **pojedynczy adres URL usługi Sign-Out** wartość, a następnie wklej ją do **adresu URL wylogowania logowania jednokrotnego**pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="336a7-154">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Single Sign-Out Service URL** value, and then paste it into the **SSO Logout URL** textbox.</span></span>
8. <span data-ttu-id="336a7-155">W **metody weryfikacji podpisu wiadomości** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="336a7-155">In the **Message Signature Verification Method** section, perform the following steps:</span></span>
   
   <span data-ttu-id="336a7-156">![Metoda weryfikacji podpisu wiadomości](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "komunikatu metodę weryfikacji podpisu")</span><span class="sxs-lookup"><span data-stu-id="336a7-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span></span>
   
  1. <span data-ttu-id="336a7-157">Wybierz **certyfikatu**.</span><span class="sxs-lookup"><span data-stu-id="336a7-157">Select **Certificate**.</span></span>
  2. <span data-ttu-id="336a7-158">Z **certyfikatu logowania jednokrotnego** listy, wybierz **RSH SHA256**.</span><span class="sxs-lookup"><span data-stu-id="336a7-158">From the **SSO Certificate** list, select **RSH SHA256**.</span></span>
  3. <span data-ttu-id="336a7-159">Utwórz plik tekstowy z pobranego certyfikatu, skopiuj zawartość pliku tekstowego, a następnie wklej go do **certyfikatu logowania jednokrotnego** pola.</span><span class="sxs-lookup"><span data-stu-id="336a7-159">Create a text file from the downloaded certificate, copy the content of the text file, and then paste it into the **SSO Certificate** field.</span></span>  
     >[!TIP]
     ><span data-ttu-id="336a7-160">Aby uzyskać więcej informacji, zobacz [sposób konwertowania binarne certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="336a7-160">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
      >  
   4. <span data-ttu-id="336a7-161">Wybierz **wyświetlone łącze do strony logowania SAMLv2**.</span><span class="sxs-lookup"><span data-stu-id="336a7-161">Select **Display a link to your SAMLv2 login page**.</span></span>
9. <span data-ttu-id="336a7-162">Kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="336a7-162">Click **Update**.</span></span>
10. <span data-ttu-id="336a7-163">W klasycznym portalu Azure, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij przycisk **Complete** zamknąć **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="336a7-163">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="336a7-164">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="336a7-164">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="336a7-165">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="336a7-165">Configure user provisioning</span></span>

<span data-ttu-id="336a7-166">Dla użytkowników usługi AAD można było zarejestrować muszą mieć przydzielone do aplikacji centralnej pulpitu.</span><span class="sxs-lookup"><span data-stu-id="336a7-166">For AAD users to be able to sign in, they must be provisioned to the Central Desktop application.</span></span> <span data-ttu-id="336a7-167">W tej sekcji opisano sposób tworzenia kont użytkowników usługi AAD w centralnej pulpitu.</span><span class="sxs-lookup"><span data-stu-id="336a7-167">This section describes how to create AAD user accounts in Central Desktop.</span></span>

<span data-ttu-id="336a7-168">**Do obsługi administracyjnej kont użytkowników do centralnej pulpitu:**</span><span class="sxs-lookup"><span data-stu-id="336a7-168">**To provision user accounts to Central Desktop:**</span></span>
1. <span data-ttu-id="336a7-169">Zaloguj się do dzierżawy centralnej pulpitu.</span><span class="sxs-lookup"><span data-stu-id="336a7-169">Log in to your Central Desktop tenant.</span></span>
2. <span data-ttu-id="336a7-170">Przejdź do **osób \> wewnętrzne elementy członkowskie**.</span><span class="sxs-lookup"><span data-stu-id="336a7-170">Go to **People \> Internal Members**.</span></span>
3. <span data-ttu-id="336a7-171">Kliknij przycisk **Dodaj wewnętrzne elementy członkowskie**.</span><span class="sxs-lookup"><span data-stu-id="336a7-171">Click **Add Internal Members**.</span></span>
   
  <span data-ttu-id="336a7-172">![Osoby](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "osób")</span><span class="sxs-lookup"><span data-stu-id="336a7-172">![People](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "People")</span></span>
4. <span data-ttu-id="336a7-173">W **wiadomości E-mail adres z nowym elementom członkowskim** tekstowym, wpisz konto usługi AAD do udostępniania, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="336a7-173">In the **Email Address of New Members** textbox, type an AAD account you want to provision, and then click **Next**.</span></span>
   
  <span data-ttu-id="336a7-174">![Adresy nowe elementy członkowskie e-mail](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "E-mail adresów nowych elementów członkowskich")</span><span class="sxs-lookup"><span data-stu-id="336a7-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span></span>
5. <span data-ttu-id="336a7-175">Kliknij przycisk **Dodaj wewnętrzne elementy członkowskie**.</span><span class="sxs-lookup"><span data-stu-id="336a7-175">Click **Add Internal member(s)**.</span></span>
   
  <span data-ttu-id="336a7-176">![Dodawanie wewnętrznego elementu członkowskiego](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "dodać wewnętrznego elementu członkowskiego")</span><span class="sxs-lookup"><span data-stu-id="336a7-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="336a7-177">Użytkownicy, dodane otrzymają wiadomość e-mail zawierającą łącze potwierdzenia, które muszą kliknij, aby aktywować konto.</span><span class="sxs-lookup"><span data-stu-id="336a7-177">The users you have added will receive an email that includes a confirmation link they need to click to activate the account.</span></span>
   > 

>[!NOTE]
><span data-ttu-id="336a7-178">Możesz użyć innych centralnej pulpitu użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez centralną pulpitu do kont użytkowników usługi AAD</span><span class="sxs-lookup"><span data-stu-id="336a7-178">You can use any other Central Desktop user account creation tools or APIs provided by Central Desktop to provision AAD user accounts</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="336a7-179">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="336a7-179">Assign users</span></span>
<span data-ttu-id="336a7-180">Aby przetestować konfigurację, musisz przyznać użytkowników usługi Azure AD, czy chcesz zezwolić, używając przypisywania do nich dostęp aplikacji do niego.</span><span class="sxs-lookup"><span data-stu-id="336a7-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="336a7-181">**Do przypisywania użytkowników do centralnej pulpitu, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="336a7-181">**To assign users to Central Desktop, perform the following steps:**</span></span>

1. <span data-ttu-id="336a7-182">W klasycznym portalu Azure Utwórz konto testu.</span><span class="sxs-lookup"><span data-stu-id="336a7-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="336a7-183">Na **centralnej pulpitu** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="336a7-183">On the **Central Desktop** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="336a7-184">![Przypisywanie użytkowników](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "przypisywanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="336a7-184">![Assign users](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assign users")</span></span>
3. <span data-ttu-id="336a7-185">Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** o potwierdzenie przypisania.</span><span class="sxs-lookup"><span data-stu-id="336a7-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="336a7-186">![Tak](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "tak")</span><span class="sxs-lookup"><span data-stu-id="336a7-186">![Yes](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="336a7-187">Jeśli chcesz przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="336a7-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="336a7-188">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="336a7-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

