---
title: 'Samouczek: Integracji Azure Active Directory z Benefitsolver | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak toouse Benefitsolver z usługą Azure Active Directory tooenable pojedynczy logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: cf4529b1-3fb6-4475-82b7-2ceedcb70b3c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 5bb8511ef9be1e386956188a93e899d6ebe56ed5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-benefitsolver"></a><span data-ttu-id="8dc2c-103">Samouczek: Integracji Azure Active Directory z Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="8dc2c-103">Tutorial: Azure Active Directory integration with Benefitsolver</span></span>
<span data-ttu-id="8dc2c-104">Celem Hello tego samouczka jest tooshow integracji hello Azure i Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-104">hello objective of this tutorial is tooshow hello integration of Azure and Benefitsolver.</span></span>  

<span data-ttu-id="8dc2c-105">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="8dc2c-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="8dc2c-106">Ważnej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="8dc2c-106">A valid Azure subscription</span></span>
* <span data-ttu-id="8dc2c-107">Benefitsolver rejestracji jednokrotnej (SSO) włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="8dc2c-107">A Benefitsolver single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="8dc2c-108">Ten samouczek użytkownicy hello Azure AD przypisano tooBenefitsolver będą mogli toosingle logowanie do aplikacji hello przy użyciu hello [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8dc2c-108">After completing this tutorial, hello Azure AD users you have assigned tooBenefitsolver will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="8dc2c-109">Scenariusz Hello opisane w tym samouczku składa się z powitania po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="8dc2c-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="8dc2c-110">Włączanie integracji aplikacji hello dla Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="8dc2c-110">Enabling hello application integration for Benefitsolver</span></span>
2. <span data-ttu-id="8dc2c-111">Konfigurowanie rejestracji jednokrotnej (SSO)</span><span class="sxs-lookup"><span data-stu-id="8dc2c-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="8dc2c-112">Konfigurowanie Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="8dc2c-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="8dc2c-113">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="8dc2c-113">Assigning users</span></span>

<span data-ttu-id="8dc2c-114">![Scenariusz](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "scenariusza")</span><span class="sxs-lookup"><span data-stu-id="8dc2c-114">![Scenario](./media/active-directory-saas-benefitsolver-tutorial/IC804820.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-benefitsolver"></a><span data-ttu-id="8dc2c-115">Włączanie integracji aplikacji hello dla Benefitsolver</span><span class="sxs-lookup"><span data-stu-id="8dc2c-115">Enabling hello application integration for Benefitsolver</span></span>
<span data-ttu-id="8dc2c-116">Celem Hello w tej sekcji jest toooutline sposób integracji aplikacji hello tooenable dla Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-116">hello objective of this section is toooutline how tooenable hello application integration for Benefitsolver.</span></span>

### <a name="tooenable-hello-application-integration-for-benefitsolver-perform-hello-following-steps"></a><span data-ttu-id="8dc2c-117">integracji aplikacji hello tooenable dla Benefitsolver, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8dc2c-117">tooenable hello application integration for Benefitsolver, perform hello following steps:</span></span>
1. <span data-ttu-id="8dc2c-118">W hello klasycznego portalu Azure, w okienku nawigacji po lewej stronie powitania kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="8dc2c-119">![Usługi Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "usługi Active Directory")</span><span class="sxs-lookup"><span data-stu-id="8dc2c-119">![Active Directory](./media/active-directory-saas-benefitsolver-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="8dc2c-120">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="8dc2c-121">Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="8dc2c-122">![Aplikacje](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "aplikacji")</span><span class="sxs-lookup"><span data-stu-id="8dc2c-122">![Applications](./media/active-directory-saas-benefitsolver-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="8dc2c-123">Kliknij przycisk **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="8dc2c-124">![Dodaj aplikację](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Dodaj aplikację")</span><span class="sxs-lookup"><span data-stu-id="8dc2c-124">![Add application](./media/active-directory-saas-benefitsolver-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="8dc2c-125">Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="8dc2c-126">![Dodawanie aplikacji z gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "dodać aplikację z gallerry")</span><span class="sxs-lookup"><span data-stu-id="8dc2c-126">![Add an application from gallerry](./media/active-directory-saas-benefitsolver-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="8dc2c-127">W hello **pole wyszukiwania**, typ **Benefitsolver**.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-127">In hello **search box**, type **Benefitsolver**.</span></span>
   
   <span data-ttu-id="8dc2c-128">![Galerii aplikacji](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "galerii aplikacji")</span><span class="sxs-lookup"><span data-stu-id="8dc2c-128">![Application Gallery](./media/active-directory-saas-benefitsolver-tutorial/IC804821.png "Application Gallery")</span></span>
7. <span data-ttu-id="8dc2c-129">Wybierz w okienku wyników hello **Benefitsolver**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-129">In hello results pane, select **Benefitsolver**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="8dc2c-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span><span class="sxs-lookup"><span data-stu-id="8dc2c-130">![Benefitssolver](./media/active-directory-saas-benefitsolver-tutorial/IC804822.png "Benefitssolver")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="8dc2c-131">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="8dc2c-131">Configure single sign-on</span></span>

<span data-ttu-id="8dc2c-132">Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooBenefitsolver do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooBenefitsolver with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="8dc2c-133">Aplikacja Benefitsolver oczekuje potwierdzenia SAML hello w określonym formacie wymaga tooyour mapowań atrybutów niestandardowych tooadd **atrybuty tokenu saml** konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-133">Your Benefitsolver application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour **saml token attributes** configuration.</span></span> 

<span data-ttu-id="8dc2c-134">powitania po zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-134">hello following screenshot shows an example for this.</span></span>

<span data-ttu-id="8dc2c-135">![Atrybuty](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "atrybutów")</span><span class="sxs-lookup"><span data-stu-id="8dc2c-135">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>

<span data-ttu-id="8dc2c-136">**tooconfigure logowanie jednokrotne, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="8dc2c-136">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="8dc2c-137">W hello klasycznego portalu Azure na powitania **Benefitsolver** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować rejestrację jednokrotną** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-137">In hello Azure classic portal, on hello **Benefitsolver** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="8dc2c-138">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="8dc2c-138">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804824.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="8dc2c-139">Na powitania **jak ma toosign użytkowników na tooBenefitsolver** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-139">On hello **How would you like users toosign on tooBenefitsolver** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="8dc2c-140">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="8dc2c-140">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804825.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="8dc2c-141">Na powitania **Konfigurowanie ustawień aplikacji** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8dc2c-141">On hello **Configure App Settings** page, perform hello following steps:</span></span>
   
   <span data-ttu-id="8dc2c-142">![Konfiguruj ustawienia aplikacji](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Konfiguruj ustawienia aplikacji")</span><span class="sxs-lookup"><span data-stu-id="8dc2c-142">![Configure App Settings](./media/active-directory-saas-benefitsolver-tutorial/IC804826.png "Configure App Settings")</span></span>
   
   1. <span data-ttu-id="8dc2c-143">W hello **na adres URL logowania** pole tekstowe, typ **http://azure.benefitsolver.com**.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-143">In hello **Sign On URL** textbox, type **http://azure.benefitsolver.com**.</span></span>
   2. <span data-ttu-id="8dc2c-144">W hello **adres URL odpowiedzi** pole tekstowe, typ **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-144">In hello **Reply URL** textbox, type **https://www.benefitsolver.com/benefits/BenefitSolverView?page_name=single_signon_saml**.</span></span>  
   3. <span data-ttu-id="8dc2c-145">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-145">Click **Next**.</span></span>
4. <span data-ttu-id="8dc2c-146">Na powitania **skonfigurować logowanie jednokrotne w Benefitsolver** strony, toodownload metadanych programu kliknij **pobierania metadanych**, a następnie zapisz plik metadanych hello lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-146">On hello **Configure single sign-on at Benefitsolver** page, toodownload your metadata, click **Download metadata**, and then save hello metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="8dc2c-147">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="8dc2c-147">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804827.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="8dc2c-148">Wyślij hello pobrać metadanych pliku tooyour Benefitsolver z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-148">Send hello downloaded metadata file tooyour Benefitsolver support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="8dc2c-149">Z zespołem pomocy technicznej Benefitsolver ma toodo hello rzeczywista konfiguracja logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-149">Your Benefitsolver support team has toodo hello actual SSO configuration.</span></span> <span data-ttu-id="8dc2c-150">Otrzymasz powiadomienie podczas logowania jednokrotnego została włączona dla Twojej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-150">You will get a notification when SSO has been enabled for your subscription.</span></span>
   >

6. <span data-ttu-id="8dc2c-151">Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete** tooclose hello **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-151">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="8dc2c-152">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="8dc2c-152">![Configure Single Sign-On](./media/active-directory-saas-benefitsolver-tutorial/IC804828.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="8dc2c-153">W menu hello na górze hello, kliknij przycisk **atrybuty** tooopen hello **atrybuty tokenu SAML** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-153">In hello menu on hello top, click **Attributes** tooopen hello **SAML Token Attributes** dialog.</span></span>
   
   <span data-ttu-id="8dc2c-154">![Atrybuty](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "atrybutów")</span><span class="sxs-lookup"><span data-stu-id="8dc2c-154">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC795920.png "Attributes")</span></span>
8. <span data-ttu-id="8dc2c-155">Mapowanie atrybutów hello wymagane tooadd, wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="8dc2c-155">tooadd hello required attribute mappings, perform hello following steps:</span></span>
   
   <span data-ttu-id="8dc2c-156">![Atrybuty](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "atrybutów")</span><span class="sxs-lookup"><span data-stu-id="8dc2c-156">![Attributes](./media/active-directory-saas-benefitsolver-tutorial/IC804823.png "Attributes")</span></span>
   
   | <span data-ttu-id="8dc2c-157">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="8dc2c-157">Attribute Name</span></span> | <span data-ttu-id="8dc2c-158">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="8dc2c-158">Attribute Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="8dc2c-159">ClientID</span><span class="sxs-lookup"><span data-stu-id="8dc2c-159">ClientID</span></span> |<span data-ttu-id="8dc2c-160">Należy tooget tej wartości z zespołem pomocy technicznej Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-160">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="8dc2c-161">ClientKey</span><span class="sxs-lookup"><span data-stu-id="8dc2c-161">ClientKey</span></span> |<span data-ttu-id="8dc2c-162">Należy tooget tej wartości z zespołem pomocy technicznej Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-162">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="8dc2c-163">LogoutURL</span><span class="sxs-lookup"><span data-stu-id="8dc2c-163">LogoutURL</span></span> |<span data-ttu-id="8dc2c-164">Należy tooget tej wartości z zespołem pomocy technicznej Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-164">You need tooget this value from your Benefitsolver support team.</span></span> |
   | <span data-ttu-id="8dc2c-165">Identyfikator pracownika</span><span class="sxs-lookup"><span data-stu-id="8dc2c-165">EmployeeID</span></span> |<span data-ttu-id="8dc2c-166">Należy tooget tej wartości z zespołem pomocy technicznej Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-166">You need tooget this value from your Benefitsolver support team.</span></span> |
   
   1. <span data-ttu-id="8dc2c-167">Dla każdego wiersza danych w powyższej tabeli powitania kliknij **Dodaj atrybut użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-167">For each data row in hello table above, click **add user attribute**.</span></span>
   2. <span data-ttu-id="8dc2c-168">W hello **nazwa atrybutu** pole tekstowe, nazwa atrybutu hello typu wyświetlany dla danego wiersza.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-168">In hello **Attribute Name** textbox, type hello attribute name shown for that row.</span></span>
   3. <span data-ttu-id="8dc2c-169">W hello **wartość atrybutu** pole tekstowe, wartość atrybutu hello wybierz wyświetlanego dla tego wiersza.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-169">In hello **Attribute Value** textbox, select hello attribute value shown for that row.</span></span>
   4. <span data-ttu-id="8dc2c-170">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="8dc2c-170">Click **Complete**.</span></span>
9. <span data-ttu-id="8dc2c-171">Kliknij przycisk **Zastosuj zmiany**.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-171">Click **Apply Changes**.</span></span>

## <a name="configure-user-provisioning"></a><span data-ttu-id="8dc2c-172">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="8dc2c-172">Configure user provisioning</span></span>
<span data-ttu-id="8dc2c-173">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Benefitsolver muszą mieć przydzielone do Benefitsolver.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-173">In order tooenable Azure AD users toolog into Benefitsolver, they must be provisioned into Benefitsolver.</span></span>  

<span data-ttu-id="8dc2c-174">W przypadku hello Benefitsolver pracownika danych jest w aplikacji wypełniać za pomocą pliku spisu z systemu HRIS (zazwyczaj co noc).</span><span class="sxs-lookup"><span data-stu-id="8dc2c-174">In hello case of Benefitsolver, employee data is in your application populated through a Census file from your HRIS system (typically nightly).</span></span>  

>[!NOTE]
><span data-ttu-id="8dc2c-175">Możesz użyć innych Benefitsolver użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Benefitsolver tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-175">You can use any other Benefitsolver user account creation tools or APIs provided by Benefitsolver tooprovision AAD user accounts.</span></span> 
> 

## <a name="assigning-users"></a><span data-ttu-id="8dc2c-176">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="8dc2c-176">Assigning users</span></span>
<span data-ttu-id="8dc2c-177">tootest konfiguracji, należy toogrant hello Azure AD użytkownicy mają tooallow przy użyciu Twojej aplikacji tooit dostępu przez przypisywanie ich.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-177">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

### <a name="tooassign-users-toobenefitsolver-perform-hello-following-steps"></a><span data-ttu-id="8dc2c-178">tooassign tooBenefitsolver użytkowników, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="8dc2c-178">tooassign users tooBenefitsolver, perform hello following steps:</span></span>
1. <span data-ttu-id="8dc2c-179">W hello klasycznego portalu Azure Utwórz konto testu.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-179">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="8dc2c-180">Na powitania ** Benefitsolver ** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-180">On hello **Benefitsolver **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="8dc2c-181">![Przypisywanie użytkowników](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "przypisywanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="8dc2c-181">![Assign Users](./media/active-directory-saas-benefitsolver-tutorial/IC804829.png "Assign Users")</span></span>
3. <span data-ttu-id="8dc2c-182">Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** tooconfirm przypisania.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-182">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="8dc2c-183">![Tak](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "tak")</span><span class="sxs-lookup"><span data-stu-id="8dc2c-183">![Yes](./media/active-directory-saas-benefitsolver-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="8dc2c-184">Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="8dc2c-184">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="8dc2c-185">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8dc2c-185">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

