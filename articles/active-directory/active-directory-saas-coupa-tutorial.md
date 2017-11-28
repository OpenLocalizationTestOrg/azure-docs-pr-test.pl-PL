---
title: 'Samouczek: Integracji Azure Active Directory z Coupa | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak toouse Coupa z usługą Azure Active Directory tooenable pojedynczy logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 87e98573718d27d408c886466a374a987f58faa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a><span data-ttu-id="11a15-103">Samouczek: Integracji Azure Active Directory z Coupa</span><span class="sxs-lookup"><span data-stu-id="11a15-103">Tutorial: Azure Active Directory integration with Coupa</span></span>
<span data-ttu-id="11a15-104">Celem Hello tego samouczka jest tooshow integracji hello Azure i Coupa.</span><span class="sxs-lookup"><span data-stu-id="11a15-104">hello objective of this tutorial is tooshow hello integration of Azure and Coupa.</span></span>  
<span data-ttu-id="11a15-105">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="11a15-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="11a15-106">Ważnej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="11a15-106">A valid Azure subscription</span></span>
* <span data-ttu-id="11a15-107">Coupa rejestracji jednokrotnej (SSO) włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="11a15-107">A Coupa single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="11a15-108">Ten samouczek użytkownicy hello Azure AD przypisano tooCoupa będą mogli toosingle logowanie do aplikacji hello przy użyciu hello [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="11a15-108">After completing this tutorial, hello Azure AD users you have assigned tooCoupa will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="11a15-109">Scenariusz Hello opisane w tym samouczku składa się z powitania po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="11a15-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="11a15-110">Włączanie integracji aplikacji hello dla Coupa</span><span class="sxs-lookup"><span data-stu-id="11a15-110">Enabling hello application integration for Coupa</span></span>
* <span data-ttu-id="11a15-111">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="11a15-111">Configuring single sign-on</span></span>
* <span data-ttu-id="11a15-112">Konfigurowanie Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="11a15-112">Configuring user provisioning</span></span>
* <span data-ttu-id="11a15-113">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="11a15-113">Assigning users</span></span>

<span data-ttu-id="11a15-114">![Scenariusz](./media/active-directory-saas-coupa-tutorial/IC791897.png "scenariusza")</span><span class="sxs-lookup"><span data-stu-id="11a15-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-coupa"></a><span data-ttu-id="11a15-115">Włącz integrację aplikacji hello dla Coupa</span><span class="sxs-lookup"><span data-stu-id="11a15-115">Enable hello application integration for Coupa</span></span>
<span data-ttu-id="11a15-116">Celem Hello w tej sekcji jest toooutline sposób integracji aplikacji hello tooenable dla Coupa.</span><span class="sxs-lookup"><span data-stu-id="11a15-116">hello objective of this section is toooutline how tooenable hello application integration for Coupa.</span></span>

<span data-ttu-id="11a15-117">**integracji aplikacji hello tooenable dla Coupa, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="11a15-117">**tooenable hello application integration for Coupa, perform hello following steps:**</span></span>

1. <span data-ttu-id="11a15-118">W hello klasycznego portalu Azure, w okienku nawigacji po lewej stronie powitania kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="11a15-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="11a15-119">![Usługi Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "usługi Active Directory")</span><span class="sxs-lookup"><span data-stu-id="11a15-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="11a15-120">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="11a15-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="11a15-121">Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="11a15-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="11a15-122">![Aplikacje](./media/active-directory-saas-coupa-tutorial/IC700994.png "aplikacji")</span><span class="sxs-lookup"><span data-stu-id="11a15-122">![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="11a15-123">Kliknij przycisk **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="11a15-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="11a15-124">![Dodaj aplikację](./media/active-directory-saas-coupa-tutorial/IC749321.png "Dodaj aplikację")</span><span class="sxs-lookup"><span data-stu-id="11a15-124">![Add application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="11a15-125">Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.</span><span class="sxs-lookup"><span data-stu-id="11a15-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="11a15-126">![Dodawanie aplikacji z gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "dodać aplikację z gallerry")</span><span class="sxs-lookup"><span data-stu-id="11a15-126">![Add an application from gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="11a15-127">W hello **pole wyszukiwania**, typ **Coupa**.</span><span class="sxs-lookup"><span data-stu-id="11a15-127">In hello **search box**, type **Coupa**.</span></span>
   
   <span data-ttu-id="11a15-128">![Galerii aplikacji](./media/active-directory-saas-coupa-tutorial/IC791898.png "galerii aplikacji")</span><span class="sxs-lookup"><span data-stu-id="11a15-128">![Application Gallery](./media/active-directory-saas-coupa-tutorial/IC791898.png "Application Gallery")</span></span>
7. <span data-ttu-id="11a15-129">Wybierz w okienku wyników hello **Coupa**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="11a15-129">In hello results pane, select **Coupa**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="11a15-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span><span class="sxs-lookup"><span data-stu-id="11a15-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="11a15-131">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="11a15-131">Configure single sign-on</span></span>

<span data-ttu-id="11a15-132">Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooCoupa do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="11a15-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooCoupa with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="11a15-133">Konfigurowanie rejestracji jednokrotnej dla Coupa wymaga tooretrieve wartość odcisku palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="11a15-133">Configuring single sign-on for Coupa requires you tooretrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="11a15-134">Jeśli nie masz doświadczenia z tej procedury, zobacz [jak tooretrieve wartość odcisku palca certyfikatu](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="11a15-134">If you are not familiar with this procedure, see [How tooretrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="11a15-135">**tooconfigure logowanie jednokrotne, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="11a15-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="11a15-136">Rejestracja tooyour Coupa witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="11a15-136">Sign on tooyour Coupa company site as an administrator.</span></span>
2. <span data-ttu-id="11a15-137">Przejdź za**Instalator \> zabezpieczeniem**.</span><span class="sxs-lookup"><span data-stu-id="11a15-137">Go too**Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="11a15-138">![Opcje zabezpieczeń](./media/active-directory-saas-coupa-tutorial/IC791900.png "środki zabezpieczające.")</span><span class="sxs-lookup"><span data-stu-id="11a15-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
3. <span data-ttu-id="11a15-139">toodownload hello Coupa metadanych pliku tooyour komputera, kliknij przycisk **pobierać i importować metadane SP**.</span><span class="sxs-lookup"><span data-stu-id="11a15-139">toodownload hello Coupa metadata file tooyour computer, click **Download and import SP metadata**.</span></span>
   
   <span data-ttu-id="11a15-140">![Metadane Coupa SP](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadanych")</span><span class="sxs-lookup"><span data-stu-id="11a15-140">![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span></span>
4. <span data-ttu-id="11a15-141">W oknie innej przeglądarki Zaloguj się na toohello klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="11a15-141">In a different browser window, sign on toohello Azure classic portal.</span></span>
5. <span data-ttu-id="11a15-142">Na powitania **Coupa** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="11a15-142">On hello **Coupa** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="11a15-143">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-coupa-tutorial/IC791902.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="11a15-143">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="11a15-144">Na powitania **jak ma toosign użytkowników na tooCoupa** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="11a15-144">On hello **How would you like users toosign on tooCoupa** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="11a15-145">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-coupa-tutorial/IC791903.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="11a15-145">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="11a15-146">Na powitania **Konfigurowanie adresu URL aplikacji** wykonaj hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="11a15-146">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
   <span data-ttu-id="11a15-147">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-coupa-tutorial/IC791904.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="11a15-147">![Configure App URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configure App URL")</span></span>   
   1. <span data-ttu-id="11a15-148">W hello **na adres URL logowania** pole tekstowe, wprowadź adres URL używany przez Twoje toosign użytkowników na tooyour Coupa aplikacji (np.: "*http://company.Coupa.com*").</span><span class="sxs-lookup"><span data-stu-id="11a15-148">In hello **Sign On URL** textbox, type URL used by your users toosign on tooyour Coupa application (e.g.: “*http://company.Coupa.com*”).</span></span>
   2. <span data-ttu-id="11a15-149">Otwórz pobrany plik metadanych Coupa, a następnie skopiuj hello **AssertionConsumerService indeksu lub adres URL**.</span><span class="sxs-lookup"><span data-stu-id="11a15-149">Open your downloaded Coupa metadata file, and then copy hello **AssertionConsumerService index/URL**.</span></span>
   3. <span data-ttu-id="11a15-150">W hello **adres URL odpowiedzi Coupa** pole tekstowe, Wklej hello **AssertionConsumerService indeksu lub adres URL** wartość.</span><span class="sxs-lookup"><span data-stu-id="11a15-150">In hello **Coupa Reply URL** textbox, paste hello **AssertionConsumerService index/URL** value.</span></span>
   4. <span data-ttu-id="11a15-151">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="11a15-151">Click **Next**.</span></span>
8. <span data-ttu-id="11a15-152">Na powitania **skonfigurować logowanie jednokrotne w Coupa** strony, toodownload pliku metadanych, kliknij przycisk **pobierania metadanych**, a następnie zapisz plik hello lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="11a15-152">On hello **Configure single sign-on at Coupa** page, toodownload your metadata file, click **Download metadata**, and then save hello file locally on your computer.</span></span>
   
   <span data-ttu-id="11a15-153">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-coupa-tutorial/IC791905.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="11a15-153">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="11a15-154">W witrynie firmy Coupa hello Przejdź zbyt**Instalator \> zabezpieczeniem**.</span><span class="sxs-lookup"><span data-stu-id="11a15-154">On hello Coupa company site, go too**Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="11a15-155">![Opcje zabezpieczeń](./media/active-directory-saas-coupa-tutorial/IC791900.png "środki zabezpieczające.")</span><span class="sxs-lookup"><span data-stu-id="11a15-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
10. <span data-ttu-id="11a15-156">W hello **Zaloguj się za pomocą poświadczeń Coupa** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="11a15-156">In hello **Log in using Coupa credentials** section, perform hello following steps:</span></span>  

   <span data-ttu-id="11a15-157">![Zaloguj się za pomocą poświadczeń Coupa](./media/active-directory-saas-coupa-tutorial/IC791906.png "Zaloguj się za pomocą poświadczeń Coupa")</span><span class="sxs-lookup"><span data-stu-id="11a15-157">![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span></span> 
   1. <span data-ttu-id="11a15-158">Wybierz **zalogowanie się przy użyciu SAML**.</span><span class="sxs-lookup"><span data-stu-id="11a15-158">Select **Log in using SAML**.</span></span>
   2. <span data-ttu-id="11a15-159">Kliknij przycisk **Przeglądaj** tooupload usługi Azure Active pobranego pliku metadanych.</span><span class="sxs-lookup"><span data-stu-id="11a15-159">Click **Browse** tooupload your downloaded Azure Active metadata file.</span></span>
   3. <span data-ttu-id="11a15-160">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="11a15-160">Click **Save**.</span></span>
11. <span data-ttu-id="11a15-161">Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete** tooclose hello **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="11a15-161">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="11a15-162">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-coupa-tutorial/IC791907.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="11a15-162">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="11a15-163">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="11a15-163">Configure user provisioning</span></span>

<span data-ttu-id="11a15-164">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable do Coupa muszą mieć przydzielone do Coupa.</span><span class="sxs-lookup"><span data-stu-id="11a15-164">In order tooenable Azure AD users toolog into Coupa, they must be provisioned into Coupa.</span></span>  

* <span data-ttu-id="11a15-165">W przypadku hello Coupa Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="11a15-165">In hello case of Coupa, provisioning is a manual task.</span></span>

<span data-ttu-id="11a15-166">**tooconfigure aprowizacji użytkowników, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="11a15-166">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="11a15-167">Zaloguj się za tooyour **Coupa** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="11a15-167">Log in tooyour **Coupa** company site as administrator.</span></span>
2. <span data-ttu-id="11a15-168">Hello menu u góry hello, kliknij przycisk **Instalator**, a następnie kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="11a15-168">In hello menu on hello top, click **Setup**, and then click **Users**.</span></span>
   
   <span data-ttu-id="11a15-169">![Użytkownicy](./media/active-directory-saas-coupa-tutorial/IC791908.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="11a15-169">![Users](./media/active-directory-saas-coupa-tutorial/IC791908.png "Users")</span></span>
3. <span data-ttu-id="11a15-170">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="11a15-170">Click **Create**.</span></span>
   
   <span data-ttu-id="11a15-171">![Tworzenie użytkowników](./media/active-directory-saas-coupa-tutorial/IC791909.png "tworzenie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="11a15-171">![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span></span>
4. <span data-ttu-id="11a15-172">W hello **Utwórz użytkownika** sekcji, wykonaj następujące kroki hello:</span><span class="sxs-lookup"><span data-stu-id="11a15-172">In hello **User Create** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="11a15-173">![Szczegóły użytkownika](./media/active-directory-saas-coupa-tutorial/IC791910.png "szczegóły użytkownika")</span><span class="sxs-lookup"><span data-stu-id="11a15-173">![User Details](./media/active-directory-saas-coupa-tutorial/IC791910.png "User Details")</span></span>
   
   1. <span data-ttu-id="11a15-174">Typ hello **logowania**, **imię**, **nazwisko**, **identyfikator rejestracji jednokrotnej**, **E-mail** atrybutów prawidłowe konto usługi Azure Active Directory, które chcesz tooprovision do hello powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="11a15-174">Type hello **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   2. <span data-ttu-id="11a15-175">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="11a15-175">Click **Create**.</span></span>   
   >[!NOTE]
   ><span data-ttu-id="11a15-176">Właściciel konta usługi Azure Active Directory Hello otrzyma wiadomość e-mail z kontem hello tooconfirm łącze zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="11a15-176">hello Azure Active Directory account holder will get an email with a link tooconfirm hello account before it becomes active.</span></span> 
   > 

>[!NOTE]
><span data-ttu-id="11a15-177">Możesz użyć innych Coupa użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Coupa tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="11a15-177">You can use any other Coupa user account creation tools or APIs provided by Coupa tooprovision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="11a15-178">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="11a15-178">Assign users</span></span>
<span data-ttu-id="11a15-179">tootest konfiguracji, należy toogrant hello Azure AD użytkownicy mają tooallow przy użyciu Twojej aplikacji tooit dostępu przez przypisywanie ich.</span><span class="sxs-lookup"><span data-stu-id="11a15-179">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="11a15-180">**tooassign tooCoupa użytkowników, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="11a15-180">**tooassign users tooCoupa, perform hello following steps:**</span></span>

1. <span data-ttu-id="11a15-181">W hello klasycznego portalu Azure Utwórz konto testu.</span><span class="sxs-lookup"><span data-stu-id="11a15-181">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="11a15-182">Na powitania ** Coupa ** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="11a15-182">On hello **Coupa **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="11a15-183">![Przypisywanie użytkowników](./media/active-directory-saas-coupa-tutorial/IC791911.png "przypisywanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="11a15-183">![Assign Users](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assign Users")</span></span>
3. <span data-ttu-id="11a15-184">Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** tooconfirm przypisania.</span><span class="sxs-lookup"><span data-stu-id="11a15-184">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="11a15-185">![Tak](./media/active-directory-saas-coupa-tutorial/IC767830.png "tak")</span><span class="sxs-lookup"><span data-stu-id="11a15-185">![Yes](./media/active-directory-saas-coupa-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="11a15-186">Jeśli chcesz tootest jednego ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="11a15-186">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="11a15-187">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="11a15-187">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

