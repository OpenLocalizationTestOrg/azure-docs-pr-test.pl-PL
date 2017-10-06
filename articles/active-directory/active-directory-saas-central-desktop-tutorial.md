---
title: "Samouczek: Integracji Azure Active Directory przy użyciu centralnej pulpitu | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse centralnej pulpitu z usługą Azure Active Directory tooenable pojedynczy logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
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
ms.openlocfilehash: 93036ae801c446ce476288c00579931ba10a843b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a><span data-ttu-id="dd218-103">Samouczek: Integracji Azure Active Directory przy użyciu centralnej pulpitu</span><span class="sxs-lookup"><span data-stu-id="dd218-103">Tutorial: Azure Active Directory integration with Central Desktop</span></span>
<span data-ttu-id="dd218-104">Celem Hello tego samouczka jest tooshow integracji hello Azure i pulpitu centralnej.</span><span class="sxs-lookup"><span data-stu-id="dd218-104">hello objective of this tutorial is tooshow hello integration of Azure and Central Desktop.</span></span> <span data-ttu-id="dd218-105">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="dd218-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="dd218-106">Ważnej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="dd218-106">A valid Azure subscription</span></span>
* <span data-ttu-id="dd218-107">Centralna pulpitu jednokrotne włączone subskrypcji / dzierżawy centralnej pulpitu</span><span class="sxs-lookup"><span data-stu-id="dd218-107">A Central desktop single sign on enabled subscription / Central desktop tenant</span></span>

<span data-ttu-id="dd218-108">Scenariusz Hello opisane w tym samouczku składa się z powitania po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="dd218-108">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="dd218-109">Włączanie integracji aplikacji hello centralnej pulpitu</span><span class="sxs-lookup"><span data-stu-id="dd218-109">Enabling hello application integration for Central Desktop</span></span>
* <span data-ttu-id="dd218-110">Konfigurowanie rejestracji jednokrotnej (SSO)</span><span class="sxs-lookup"><span data-stu-id="dd218-110">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="dd218-111">Konfigurowanie Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="dd218-111">Configuring user provisioning</span></span>
* <span data-ttu-id="dd218-112">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="dd218-112">Assigning users</span></span>

<span data-ttu-id="dd218-113">![Scenariusz](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "scenariusza")</span><span class="sxs-lookup"><span data-stu-id="dd218-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-central-desktop"></a><span data-ttu-id="dd218-114">Włącz integrację aplikacji hello centralnej pulpitu</span><span class="sxs-lookup"><span data-stu-id="dd218-114">Enable hello application integration for Central Desktop</span></span>
<span data-ttu-id="dd218-115">Celem Hello w tej sekcji jest toooutline sposób integracji aplikacji hello tooenable centralnej pulpitu.</span><span class="sxs-lookup"><span data-stu-id="dd218-115">hello objective of this section is toooutline how tooenable hello application integration for Central Desktop.</span></span>

<span data-ttu-id="dd218-116">**Integracja aplikacji hello tooenable centralnej pulpitu, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="dd218-116">**tooenable hello application integration for Central Desktop, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd218-117">W hello klasycznego portalu Azure, w okienku nawigacji po lewej stronie powitania kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dd218-117">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="dd218-118">![Usługi Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "usługi Active Directory")</span><span class="sxs-lookup"><span data-stu-id="dd218-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="dd218-119">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="dd218-119">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="dd218-120">Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="dd218-120">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="dd218-121">![Aplikacje](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "aplikacji")</span><span class="sxs-lookup"><span data-stu-id="dd218-121">![Applications](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="dd218-122">Kliknij przycisk **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="dd218-122">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="dd218-123">![Dodaj aplikację](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Dodaj aplikację")</span><span class="sxs-lookup"><span data-stu-id="dd218-123">![Add application](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="dd218-124">Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.</span><span class="sxs-lookup"><span data-stu-id="dd218-124">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="dd218-125">![Dodawanie aplikacji z gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "dodać aplikację z gallerry")</span><span class="sxs-lookup"><span data-stu-id="dd218-125">![Add an application from gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="dd218-126">W hello **pole wyszukiwania**, typ **centralnej pulpitu**.</span><span class="sxs-lookup"><span data-stu-id="dd218-126">In hello **search box**, type **Central Desktop**.</span></span>
   
   <span data-ttu-id="dd218-127">![Galerii aplikacji](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "galerii aplikacji")</span><span class="sxs-lookup"><span data-stu-id="dd218-127">![Application gallery](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Application gallery")</span></span>
7. <span data-ttu-id="dd218-128">Wybierz w okienku wyników hello **centralnej pulpitu**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="dd218-128">In hello results pane, select **Central Desktop**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="dd218-129">![Centralna pulpitu](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "centralnej pulpitu")</span><span class="sxs-lookup"><span data-stu-id="dd218-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="dd218-130">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="dd218-130">Configure single sign-on</span></span>

<span data-ttu-id="dd218-131">Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooCentral pulpitu do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="dd218-131">hello objective of this section is toooutline how tooenable users tooauthenticate tooCentral Desktop with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="dd218-132">W ramach tej procedury jest wymagana tooupload dzierżawcy centralnej pulpitu tooyour base-64 zakodowanego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="dd218-132">As part of this procedure, you are required tooupload a base-64 encoded certificate tooyour Central Desktop tenant.</span></span>  
<span data-ttu-id="dd218-133">Jeśli nie masz doświadczenia z tej procedury, zobacz [jak tooconvert pliku binarnego certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="dd218-133">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="dd218-134">**tooconfigure logowanie jednokrotne, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="dd218-134">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd218-135">W hello klasycznego portalu Azure na powitania **centralnej pulpitu** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello ** skonfigurować rejestrację jednokrotną ** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dd218-135">In hello Azure classic portal, on hello **Central Desktop** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
   <span data-ttu-id="dd218-136">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="dd218-136">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="dd218-137">Na powitania **jak ma toosign użytkowników na pulpicie tooCentral** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="dd218-137">On hello **How would you like users toosign on tooCentral Desktop** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="dd218-138">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="dd218-138">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="dd218-139">Na powitania **Konfigurowanie adresu URL aplikacji** , wykonaj następujące kroki hello, a następnie kliknij przycisk **dalej**:</span><span class="sxs-lookup"><span data-stu-id="dd218-139">On hello **Configure App URL** page, perform hello following steps, and then click **Next**:</span></span> 
   
   1. <span data-ttu-id="dd218-140">W hello **centralnej pulpitu adres URL logowania** pole tekstowe, wprowadź adres URL hello dzierżawy centralnej pulpitu (np.: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="dd218-140">In hello **Central Desktop Sign In URL** textbox, type hello URL of your Central Desktop tenant (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   2. <span data-ttu-id="dd218-141">W polu tekstowym adres URL odpowiedzi pulpitu Central hello, wpisz adres URL centralnej AssertionConsumerService pulpitu (np.: https://contoso.centraldesktop.com/saml2-assertion.php).</span><span class="sxs-lookup"><span data-stu-id="dd218-141">In hello Central  Desktop Reply URL textbox, type your Central Desktop AssertionConsumerService URL (e.g.:  https://contoso.centraldesktop.com/saml2-assertion.php).</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="dd218-142">Można pobrać wartości hello z hello centralnej pulpitu metadanych (np.: *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="dd218-142">You can get hello value from hello central desktop metadata (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   >  
   
   <span data-ttu-id="dd218-143">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="dd218-143">![Configure app URL](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configure app URL")</span></span>
4. <span data-ttu-id="dd218-144">Na powitania **skonfigurować logowanie jednokrotne w centralnej pulpitu** strony, toodownload certyfikat, kliknij przycisk **pobierania certyfikatu**, a następnie zapisz plik certyfikatu hello na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="dd218-144">On hello **Configure single sign-on at Central Desktop** page, toodownload your certificate, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
  <span data-ttu-id="dd218-145">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="dd218-145">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="dd218-146">Zaloguj się za tooyour **centralnej pulpitu** dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="dd218-146">Log in tooyour **Central Desktop** tenant.</span></span>
6. <span data-ttu-id="dd218-147">Przejdź za**ustawienia**, kliknij przycisk **zaawansowane**, a następnie kliknij przycisk **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="dd218-147">Go too**Settings**, click **Advanced**, and then click **Single Sign On**.</span></span>
   
  <span data-ttu-id="dd218-148">![Instalator — zaawansowane](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Instalator — zaawansowane")</span><span class="sxs-lookup"><span data-stu-id="dd218-148">![Setup - Advanced](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span></span>
7. <span data-ttu-id="dd218-149">Na powitania **pojedynczy znak na ustawienia** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="dd218-149">On hello **Single Sign On Settings** page, perform hello following steps:</span></span>
   
  <span data-ttu-id="dd218-150">![Rejestracja jednokrotna ustawień](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Rejestracja jednokrotna ustawień")</span><span class="sxs-lookup"><span data-stu-id="dd218-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span></span>
   
  1. <span data-ttu-id="dd218-151">Wybierz **Włącz SAML v2 logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="dd218-151">Select **Enable SAML v2 Single Sign On**.</span></span>
  2. <span data-ttu-id="dd218-152">W hello klasycznego portalu Azure na powitania **skonfigurować logowanie jednokrotne w centralnej pulpitu** strony, hello kopiowania **adres URL wystawcy** wartość, a następnie wklej go do hello **adres URL logowania jednokrotnego** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="dd218-152">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Issuer URL** value, and then paste it into hello **SSO URL** textbox.</span></span>
  3. <span data-ttu-id="dd218-153">W hello klasycznego portalu Azure na powitania **skonfigurować logowanie jednokrotne w centralnej pulpitu** strony, hello kopiowania **zdalnego adresu URL logowania** wartość, a następnie wklej go do hello **adres URL logowania jednokrotnego logowania**pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="dd218-153">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Remote Login URL** value, and then paste it into hello **SSO Login URL** textbox.</span></span>
  4. <span data-ttu-id="dd218-154">W hello klasycznego portalu Azure na powitania **skonfigurować logowanie jednokrotne w centralnej pulpitu** strony, hello kopiowania **pojedynczy adres URL usługi Sign-Out** wartość, a następnie wklej go do hello **adresu URL wylogowania logowania jednokrotnego** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="dd218-154">In hello Azure classic portal, on hello **Configure single sign-on at Central Desktop** page, copy hello **Single Sign-Out Service URL** value, and then paste it into hello **SSO Logout URL** textbox.</span></span>
8. <span data-ttu-id="dd218-155">W hello **metody weryfikacji podpisu wiadomości** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="dd218-155">In hello **Message Signature Verification Method** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="dd218-156">![Metoda weryfikacji podpisu wiadomości](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "komunikatu metodę weryfikacji podpisu")</span><span class="sxs-lookup"><span data-stu-id="dd218-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span></span>
   
  1. <span data-ttu-id="dd218-157">Wybierz **certyfikatu**.</span><span class="sxs-lookup"><span data-stu-id="dd218-157">Select **Certificate**.</span></span>
  2. <span data-ttu-id="dd218-158">Z hello **certyfikatu logowania jednokrotnego** listy, wybierz **RSH SHA256**.</span><span class="sxs-lookup"><span data-stu-id="dd218-158">From hello **SSO Certificate** list, select **RSH SHA256**.</span></span>
  3. <span data-ttu-id="dd218-159">Utwórz plik tekstowy z certyfikatu hello pobrane, hello kopiowania zawartości z pliku tekstowego hello, a następnie wklej go do hello **certyfikatu logowania jednokrotnego** pola.</span><span class="sxs-lookup"><span data-stu-id="dd218-159">Create a text file from hello downloaded certificate, copy hello content of hello text file, and then paste it into hello **SSO Certificate** field.</span></span>  
     >[!TIP]
     ><span data-ttu-id="dd218-160">Aby uzyskać więcej informacji, zobacz [jak tooconvert pliku binarnego certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="dd218-160">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
      >  
   4. <span data-ttu-id="dd218-161">Wybierz **wyświetlenia strony logowania łącze tooyour SAMLv2**.</span><span class="sxs-lookup"><span data-stu-id="dd218-161">Select **Display a link tooyour SAMLv2 login page**.</span></span>
9. <span data-ttu-id="dd218-162">Kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="dd218-162">Click **Update**.</span></span>
10. <span data-ttu-id="dd218-163">Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete** tooclose hello **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="dd218-163">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="dd218-164">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="dd218-164">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="dd218-165">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="dd218-165">Configure user provisioning</span></span>

<span data-ttu-id="dd218-166">AAD użytkowników toobe stanie toosign w muszą być elastycznie toohello aplikacji centralnej pulpitu.</span><span class="sxs-lookup"><span data-stu-id="dd218-166">For AAD users toobe able toosign in, they must be provisioned toohello Central Desktop application.</span></span> <span data-ttu-id="dd218-167">W tej sekcji opisano, jak konta użytkowników usługi AAD toocreate w centralnej pulpitu.</span><span class="sxs-lookup"><span data-stu-id="dd218-167">This section describes how toocreate AAD user accounts in Central Desktop.</span></span>

<span data-ttu-id="dd218-168">**tooCentral kont użytkownika tooprovision pulpitu:**</span><span class="sxs-lookup"><span data-stu-id="dd218-168">**tooprovision user accounts tooCentral Desktop:**</span></span>
1. <span data-ttu-id="dd218-169">Zaloguj się za tooyour dzierżawy centralnej pulpitu.</span><span class="sxs-lookup"><span data-stu-id="dd218-169">Log in tooyour Central Desktop tenant.</span></span>
2. <span data-ttu-id="dd218-170">Przejdź za**osób \> wewnętrzne elementy członkowskie**.</span><span class="sxs-lookup"><span data-stu-id="dd218-170">Go too**People \> Internal Members**.</span></span>
3. <span data-ttu-id="dd218-171">Kliknij przycisk **Dodaj wewnętrzne elementy członkowskie**.</span><span class="sxs-lookup"><span data-stu-id="dd218-171">Click **Add Internal Members**.</span></span>
   
  <span data-ttu-id="dd218-172">![Osoby](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "osób")</span><span class="sxs-lookup"><span data-stu-id="dd218-172">![People](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "People")</span></span>
4. <span data-ttu-id="dd218-173">W hello **wiadomości E-mail adres z nowym elementom członkowskim** tekstowym, wpisz konto usługi AAD tooprovision, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="dd218-173">In hello **Email Address of New Members** textbox, type an AAD account you want tooprovision, and then click **Next**.</span></span>
   
  <span data-ttu-id="dd218-174">![Adresy nowe elementy członkowskie e-mail](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "E-mail adresów nowych elementów członkowskich")</span><span class="sxs-lookup"><span data-stu-id="dd218-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span></span>
5. <span data-ttu-id="dd218-175">Kliknij przycisk **Dodaj wewnętrzne elementy członkowskie**.</span><span class="sxs-lookup"><span data-stu-id="dd218-175">Click **Add Internal member(s)**.</span></span>
   
  <span data-ttu-id="dd218-176">![Dodawanie wewnętrznego elementu członkowskiego](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "dodać wewnętrznego elementu członkowskiego")</span><span class="sxs-lookup"><span data-stu-id="dd218-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="dd218-177">Użytkownicy Hello, dodane otrzymają wiadomość e-mail zawierającą link potwierdzenia muszą tooclick tooactivate hello konta.</span><span class="sxs-lookup"><span data-stu-id="dd218-177">hello users you have added will receive an email that includes a confirmation link they need tooclick tooactivate hello account.</span></span>
   > 

>[!NOTE]
><span data-ttu-id="dd218-178">Możesz użyć innych centralnej pulpitu użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez centralną pulpitu tooprovision kont użytkowników usługi AAD</span><span class="sxs-lookup"><span data-stu-id="dd218-178">You can use any other Central Desktop user account creation tools or APIs provided by Central Desktop tooprovision AAD user accounts</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="dd218-179">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="dd218-179">Assign users</span></span>
<span data-ttu-id="dd218-180">tootest konfiguracji, należy toogrant hello Azure AD użytkownicy mają tooallow przy użyciu Twojej aplikacji tooit dostępu przez przypisywanie ich.</span><span class="sxs-lookup"><span data-stu-id="dd218-180">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="dd218-181">**tooassign tooCentral Użytkownicy pulpitu, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="dd218-181">**tooassign users tooCentral Desktop, perform hello following steps:**</span></span>

1. <span data-ttu-id="dd218-182">W hello klasycznego portalu Azure Utwórz konto testu.</span><span class="sxs-lookup"><span data-stu-id="dd218-182">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="dd218-183">Na powitania **centralnej pulpitu** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="dd218-183">On hello **Central Desktop** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="dd218-184">![Przypisywanie użytkowników](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "przypisywanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="dd218-184">![Assign users](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assign users")</span></span>
3. <span data-ttu-id="dd218-185">Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** tooconfirm przypisania.</span><span class="sxs-lookup"><span data-stu-id="dd218-185">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="dd218-186">![Tak](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "tak")</span><span class="sxs-lookup"><span data-stu-id="dd218-186">![Yes](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="dd218-187">Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="dd218-187">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="dd218-188">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dd218-188">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

