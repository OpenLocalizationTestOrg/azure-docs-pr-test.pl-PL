---
title: 'Samouczek: Integracji Azure Active Directory z Coupa | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak używać Coupa usłudze Azure Active Directory w celu włączenia logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
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
ms.openlocfilehash: c952975919cfd948f1b9ea93ff2ac2641a53f923
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a><span data-ttu-id="5ff51-103">Samouczek: Integracji Azure Active Directory z Coupa</span><span class="sxs-lookup"><span data-stu-id="5ff51-103">Tutorial: Azure Active Directory integration with Coupa</span></span>
<span data-ttu-id="5ff51-104">Celem tego samouczka jest pokazanie integracji Azure i Coupa.</span><span class="sxs-lookup"><span data-stu-id="5ff51-104">The objective of this tutorial is to show the integration of Azure and Coupa.</span></span>  
<span data-ttu-id="5ff51-105">Scenariusz opisany w tym samouczku założono, że już następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5ff51-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="5ff51-106">Ważnej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="5ff51-106">A valid Azure subscription</span></span>
* <span data-ttu-id="5ff51-107">Coupa rejestracji jednokrotnej (SSO) włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="5ff51-107">A Coupa single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="5ff51-108">Ten samouczek użytkowników usługi Azure AD, zostały przypisane do Coupa będzie można funkcji logowania jednokrotnego do aplikacji przy użyciu [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5ff51-108">After completing this tutorial, the Azure AD users you have assigned to Coupa will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="5ff51-109">Scenariusz opisany w tym samouczku składa się z następujących bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="5ff51-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="5ff51-110">Włączanie integracji aplikacji dla Coupa</span><span class="sxs-lookup"><span data-stu-id="5ff51-110">Enabling the application integration for Coupa</span></span>
* <span data-ttu-id="5ff51-111">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5ff51-111">Configuring single sign-on</span></span>
* <span data-ttu-id="5ff51-112">Konfigurowanie Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="5ff51-112">Configuring user provisioning</span></span>
* <span data-ttu-id="5ff51-113">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="5ff51-113">Assigning users</span></span>

<span data-ttu-id="5ff51-114">![Scenariusz](./media/active-directory-saas-coupa-tutorial/IC791897.png "scenariusza")</span><span class="sxs-lookup"><span data-stu-id="5ff51-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-coupa"></a><span data-ttu-id="5ff51-115">Włącz integrację aplikacji dla Coupa</span><span class="sxs-lookup"><span data-stu-id="5ff51-115">Enable the application integration for Coupa</span></span>
<span data-ttu-id="5ff51-116">Celem tej sekcji jest przedstawiają sposób włączania integracji aplikacji dla Coupa.</span><span class="sxs-lookup"><span data-stu-id="5ff51-116">The objective of this section is to outline how to enable the application integration for Coupa.</span></span>

<span data-ttu-id="5ff51-117">**Aby włączyć integrację aplikacji dla Coupa, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5ff51-117">**To enable the application integration for Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="5ff51-118">W klasycznym portalu Azure, w okienku nawigacji po lewej stronie kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5ff51-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="5ff51-119">![Usługi Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "usługi Active Directory")</span><span class="sxs-lookup"><span data-stu-id="5ff51-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="5ff51-120">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="5ff51-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="5ff51-121">Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="5ff51-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="5ff51-122">![Aplikacje](./media/active-directory-saas-coupa-tutorial/IC700994.png "aplikacji")</span><span class="sxs-lookup"><span data-stu-id="5ff51-122">![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="5ff51-123">Kliknij przycisk **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="5ff51-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="5ff51-124">![Dodaj aplikację](./media/active-directory-saas-coupa-tutorial/IC749321.png "Dodaj aplikację")</span><span class="sxs-lookup"><span data-stu-id="5ff51-124">![Add application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="5ff51-125">Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.</span><span class="sxs-lookup"><span data-stu-id="5ff51-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="5ff51-126">![Dodawanie aplikacji z gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "dodać aplikację z gallerry")</span><span class="sxs-lookup"><span data-stu-id="5ff51-126">![Add an application from gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="5ff51-127">W **pole wyszukiwania**, typ **Coupa**.</span><span class="sxs-lookup"><span data-stu-id="5ff51-127">In the **search box**, type **Coupa**.</span></span>
   
   <span data-ttu-id="5ff51-128">![Galerii aplikacji](./media/active-directory-saas-coupa-tutorial/IC791898.png "galerii aplikacji")</span><span class="sxs-lookup"><span data-stu-id="5ff51-128">![Application Gallery](./media/active-directory-saas-coupa-tutorial/IC791898.png "Application Gallery")</span></span>
7. <span data-ttu-id="5ff51-129">W okienku wyników wybierz **Coupa**, a następnie kliknij przycisk **Complete** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="5ff51-129">In the results pane, select **Coupa**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="5ff51-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span><span class="sxs-lookup"><span data-stu-id="5ff51-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="5ff51-131">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5ff51-131">Configure single sign-on</span></span>

<span data-ttu-id="5ff51-132">Celem tej sekcji jest przedstawiają sposób umożliwić użytkownikom uwierzytelnianie na Coupa do swojego konta w usłudze Azure AD przy użyciu federacyjnego na podstawie protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="5ff51-132">The objective of this section is to outline how to enable users to authenticate to Coupa with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="5ff51-133">Konfigurowanie rejestracji jednokrotnej dla Coupa należy pobrać wartość odcisku palca certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="5ff51-133">Configuring single sign-on for Coupa requires you to retrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="5ff51-134">Jeśli nie masz doświadczenia z tej procedury, zobacz [jak pobrać wartość odcisku palca certyfikatu](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="5ff51-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="5ff51-135">**Aby skonfigurować rejestrację jednokrotną, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5ff51-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="5ff51-136">Zalogować się do witryny firmy Coupa jako administrator.</span><span class="sxs-lookup"><span data-stu-id="5ff51-136">Sign on to your Coupa company site as an administrator.</span></span>
2. <span data-ttu-id="5ff51-137">Przejdź do **Instalator \> zabezpieczeniem**.</span><span class="sxs-lookup"><span data-stu-id="5ff51-137">Go to **Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="5ff51-138">![Opcje zabezpieczeń](./media/active-directory-saas-coupa-tutorial/IC791900.png "środki zabezpieczające.")</span><span class="sxs-lookup"><span data-stu-id="5ff51-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
3. <span data-ttu-id="5ff51-139">Aby pobrać pliku metadanych Coupa do komputera, kliknij przycisk **pobieranie i Importowanie metadanych SP**.</span><span class="sxs-lookup"><span data-stu-id="5ff51-139">To download the Coupa metadata file to your computer, click **Download and import SP metadata**.</span></span>
   
   <span data-ttu-id="5ff51-140">![Metadane Coupa SP](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadanych")</span><span class="sxs-lookup"><span data-stu-id="5ff51-140">![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span></span>
4. <span data-ttu-id="5ff51-141">W oknie innej przeglądarki należy zalogować się do klasycznego portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="5ff51-141">In a different browser window, sign on to the Azure classic portal.</span></span>
5. <span data-ttu-id="5ff51-142">Na **Coupa** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5ff51-142">On the **Coupa** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="5ff51-143">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-coupa-tutorial/IC791902.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5ff51-143">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="5ff51-144">Na **jak chcesz użytkownikom zalogować się na Coupa** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="5ff51-144">On the **How would you like users to sign on to Coupa** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="5ff51-145">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-coupa-tutorial/IC791903.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5ff51-145">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="5ff51-146">Na **Konfigurowanie adresu URL aplikacji** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5ff51-146">On the **Configure App URL** page, perform the following steps:</span></span>
   
   <span data-ttu-id="5ff51-147">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-coupa-tutorial/IC791904.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="5ff51-147">![Configure App URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configure App URL")</span></span>   
   1. <span data-ttu-id="5ff51-148">W **na adres URL logowania** pole tekstowe, wprowadź adres URL używany przez użytkowników do logowania do aplikacji Coupa (np.: "*http://company.Coupa.com*").</span><span class="sxs-lookup"><span data-stu-id="5ff51-148">In the **Sign On URL** textbox, type URL used by your users to sign on to your Coupa application (e.g.: “*http://company.Coupa.com*”).</span></span>
   2. <span data-ttu-id="5ff51-149">Otwórz pobrany plik metadanych Coupa, a następnie skopiuj **AssertionConsumerService indeksu lub adres URL**.</span><span class="sxs-lookup"><span data-stu-id="5ff51-149">Open your downloaded Coupa metadata file, and then copy the **AssertionConsumerService index/URL**.</span></span>
   3. <span data-ttu-id="5ff51-150">W **adres URL odpowiedzi Coupa** pole tekstowe, Wklej **AssertionConsumerService indeksu lub adres URL** wartość.</span><span class="sxs-lookup"><span data-stu-id="5ff51-150">In the **Coupa Reply URL** textbox, paste the **AssertionConsumerService index/URL** value.</span></span>
   4. <span data-ttu-id="5ff51-151">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="5ff51-151">Click **Next**.</span></span>
8. <span data-ttu-id="5ff51-152">Na **skonfigurować logowanie jednokrotne w Coupa** można pobrać pliku metadanych, kliknij przycisk **pobierania metadanych**, a następnie zapisz plik lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="5ff51-152">On the **Configure single sign-on at Coupa** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
   
   <span data-ttu-id="5ff51-153">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-coupa-tutorial/IC791905.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5ff51-153">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="5ff51-154">W witrynie firmy Coupa, przejdź do **Instalator \> zabezpieczeniem**.</span><span class="sxs-lookup"><span data-stu-id="5ff51-154">On the Coupa company site, go to **Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="5ff51-155">![Opcje zabezpieczeń](./media/active-directory-saas-coupa-tutorial/IC791900.png "środki zabezpieczające.")</span><span class="sxs-lookup"><span data-stu-id="5ff51-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
10. <span data-ttu-id="5ff51-156">W **Zaloguj się za pomocą poświadczeń Coupa** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5ff51-156">In the **Log in using Coupa credentials** section, perform the following steps:</span></span>  

   <span data-ttu-id="5ff51-157">![Zaloguj się za pomocą poświadczeń Coupa](./media/active-directory-saas-coupa-tutorial/IC791906.png "Zaloguj się za pomocą poświadczeń Coupa")</span><span class="sxs-lookup"><span data-stu-id="5ff51-157">![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span></span> 
   1. <span data-ttu-id="5ff51-158">Wybierz **zalogowanie się przy użyciu SAML**.</span><span class="sxs-lookup"><span data-stu-id="5ff51-158">Select **Log in using SAML**.</span></span>
   2. <span data-ttu-id="5ff51-159">Kliknij przycisk **Przeglądaj** przekazać pobranego pliku metadanych usługi Azure Active.</span><span class="sxs-lookup"><span data-stu-id="5ff51-159">Click **Browse** to upload your downloaded Azure Active metadata file.</span></span>
   3. <span data-ttu-id="5ff51-160">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="5ff51-160">Click **Save**.</span></span>
11. <span data-ttu-id="5ff51-161">W klasycznym portalu Azure, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij przycisk **Complete** zamknąć **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5ff51-161">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="5ff51-162">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-coupa-tutorial/IC791907.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5ff51-162">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="5ff51-163">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="5ff51-163">Configure user provisioning</span></span>

<span data-ttu-id="5ff51-164">Aby włączyć użytkowników usługi Azure AD zalogować się do Coupa, musi być przygotowana do Coupa.</span><span class="sxs-lookup"><span data-stu-id="5ff51-164">In order to enable Azure AD users to log into Coupa, they must be provisioned into Coupa.</span></span>  

* <span data-ttu-id="5ff51-165">W przypadku Coupa Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="5ff51-165">In the case of Coupa, provisioning is a manual task.</span></span>

<span data-ttu-id="5ff51-166">**Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5ff51-166">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="5ff51-167">Zaloguj się do Twojego **Coupa** witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="5ff51-167">Log in to your **Coupa** company site as administrator.</span></span>
2. <span data-ttu-id="5ff51-168">W menu u góry kliknij **Instalator**, a następnie kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="5ff51-168">In the menu on the top, click **Setup**, and then click **Users**.</span></span>
   
   <span data-ttu-id="5ff51-169">![Użytkownicy](./media/active-directory-saas-coupa-tutorial/IC791908.png "użytkowników")</span><span class="sxs-lookup"><span data-stu-id="5ff51-169">![Users](./media/active-directory-saas-coupa-tutorial/IC791908.png "Users")</span></span>
3. <span data-ttu-id="5ff51-170">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5ff51-170">Click **Create**.</span></span>
   
   <span data-ttu-id="5ff51-171">![Tworzenie użytkowników](./media/active-directory-saas-coupa-tutorial/IC791909.png "tworzenie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="5ff51-171">![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span></span>
4. <span data-ttu-id="5ff51-172">W **Utwórz użytkownika** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5ff51-172">In the **User Create** section, perform the following steps:</span></span>
   
   <span data-ttu-id="5ff51-173">![Szczegóły użytkownika](./media/active-directory-saas-coupa-tutorial/IC791910.png "szczegóły użytkownika")</span><span class="sxs-lookup"><span data-stu-id="5ff51-173">![User Details](./media/active-directory-saas-coupa-tutorial/IC791910.png "User Details")</span></span>
   
   1. <span data-ttu-id="5ff51-174">Typ **logowania**, **imię**, **nazwisko**, **identyfikator rejestracji jednokrotnej**, **E-mail** atrybutów prawidłowe konto usługi Azure Active Directory, które chcesz udostępnić do powiązanych pól tekstowych.</span><span class="sxs-lookup"><span data-stu-id="5ff51-174">Type the **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="5ff51-175">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5ff51-175">Click **Create**.</span></span>   
   >[!NOTE]
   ><span data-ttu-id="5ff51-176">Właściciel konta usługi Azure Active Directory otrzyma wiadomość e-mail z łączem do potwierdzenia konta, zanim staje się aktywny.</span><span class="sxs-lookup"><span data-stu-id="5ff51-176">The Azure Active Directory account holder will get an email with a link to confirm the account before it becomes active.</span></span> 
   > 

>[!NOTE]
><span data-ttu-id="5ff51-177">Możesz użyć innych Coupa użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez Coupa do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="5ff51-177">You can use any other Coupa user account creation tools or APIs provided by Coupa to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="5ff51-178">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="5ff51-178">Assign users</span></span>
<span data-ttu-id="5ff51-179">Aby przetestować konfigurację, musisz przyznać użytkowników usługi Azure AD, czy chcesz zezwolić, używając przypisywania do nich dostęp aplikacji do niego.</span><span class="sxs-lookup"><span data-stu-id="5ff51-179">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="5ff51-180">**Do przypisywania użytkowników do Coupa, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5ff51-180">**To assign users to Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="5ff51-181">W klasycznym portalu Azure Utwórz konto testu.</span><span class="sxs-lookup"><span data-stu-id="5ff51-181">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="5ff51-182">Na ** Coupa ** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="5ff51-182">On the **Coupa **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="5ff51-183">![Przypisywanie użytkowników](./media/active-directory-saas-coupa-tutorial/IC791911.png "przypisywanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="5ff51-183">![Assign Users](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assign Users")</span></span>
3. <span data-ttu-id="5ff51-184">Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** o potwierdzenie przypisania.</span><span class="sxs-lookup"><span data-stu-id="5ff51-184">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="5ff51-185">![Tak](./media/active-directory-saas-coupa-tutorial/IC767830.png "tak")</span><span class="sxs-lookup"><span data-stu-id="5ff51-185">![Yes](./media/active-directory-saas-coupa-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="5ff51-186">Jeśli chcesz przetestować jednego ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="5ff51-186">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="5ff51-187">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5ff51-187">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

