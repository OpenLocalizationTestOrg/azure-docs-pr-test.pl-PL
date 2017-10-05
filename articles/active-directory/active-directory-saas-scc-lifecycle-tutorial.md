---
title: "Samouczek: Azure Active Directory integrację z cyklem życia SCC | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak użyć SCC cyklu życia z usługą Azure Active Directory w celu włączenia logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 9748bf38-ffc3-4d51-a1ae-207ce57104fa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 9a30bcca720ff135d0180d73f46e78403e9bca43
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="053ab-103">Samouczek: Azure Active Directory integrację z cyklem życia SCC</span><span class="sxs-lookup"><span data-stu-id="053ab-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>
<span data-ttu-id="053ab-104">Celem tego samouczka jest pokazanie integracji Azure i SCC cyklu życia.</span><span class="sxs-lookup"><span data-stu-id="053ab-104">The objective of this tutorial is to show the integration of Azure and SCC LifeCycle.</span></span>  

<span data-ttu-id="053ab-105">Scenariusz opisany w tym samouczku założono, że już następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="053ab-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="053ab-106">Ważnej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="053ab-106">A valid Azure subscription</span></span>
* <span data-ttu-id="053ab-107">Cykl życia SCC rejestracji jednokrotnej (SSO) włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="053ab-107">A SCC LifeCycle single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="053ab-108">Ten samouczek użytkowników usługi Azure AD, zostały przypisane do cyklu życia SCC będzie można funkcji logowania jednokrotnego do aplikacji w witrynie firmy SCC cyklu życia (usługa zainicjował dostawcy logowania) lub przy użyciu [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="053ab-108">After completing this tutorial, the Azure AD users you have assigned to SCC LifeCycle will be able to single sign into the application at your SCC LifeCycle company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="053ab-109">Scenariusz opisany w tym samouczku składa się z następujących bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="053ab-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

1. <span data-ttu-id="053ab-110">Włączanie integracji aplikacji dla SCC cykl życia</span><span class="sxs-lookup"><span data-stu-id="053ab-110">Enabling the application integration for SCC LifeCycle</span></span>
2. <span data-ttu-id="053ab-111">Konfigurowanie rejestracji jednokrotnej (SSO)</span><span class="sxs-lookup"><span data-stu-id="053ab-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="053ab-112">Konfigurowanie Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="053ab-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="053ab-113">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="053ab-113">Assigning users</span></span>

<span data-ttu-id="053ab-114">![Scenariusz](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "scenariusza")</span><span class="sxs-lookup"><span data-stu-id="053ab-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-scc-lifecycle"></a><span data-ttu-id="053ab-115">Włącz integrację aplikacji dla SCC cykl życia</span><span class="sxs-lookup"><span data-stu-id="053ab-115">Enable the application integration for SCC LifeCycle</span></span>
<span data-ttu-id="053ab-116">Celem tej sekcji jest przedstawiają sposób włączania integracji aplikacji dla SCC cyklu życia.</span><span class="sxs-lookup"><span data-stu-id="053ab-116">The objective of this section is to outline how to enable the application integration for SCC LifeCycle.</span></span>

<span data-ttu-id="053ab-117">**Aby włączyć integrację aplikacji dla cyklu życia SCC, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="053ab-117">**To enable the application integration for SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="053ab-118">W klasycznym portalu Azure, w okienku nawigacji po lewej stronie kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="053ab-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="053ab-119">![Usługi Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "usługi Active Directory")</span><span class="sxs-lookup"><span data-stu-id="053ab-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="053ab-120">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="053ab-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="053ab-121">Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="053ab-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    <span data-ttu-id="053ab-122">![Aplikacje](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "aplikacji")</span><span class="sxs-lookup"><span data-stu-id="053ab-122">![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="053ab-123">Kliknij przycisk **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="053ab-123">Click **Add** at the bottom of the page.</span></span>
   
    <span data-ttu-id="053ab-124">![Dodaj aplikację](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Dodaj aplikację")</span><span class="sxs-lookup"><span data-stu-id="053ab-124">![Add application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="053ab-125">Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.</span><span class="sxs-lookup"><span data-stu-id="053ab-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    <span data-ttu-id="053ab-126">![Dodawanie aplikacji z gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "dodać aplikację z gallerry")</span><span class="sxs-lookup"><span data-stu-id="053ab-126">![Add an application from gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="053ab-127">W **pole wyszukiwania**, typ **cyklu życia SCC**.</span><span class="sxs-lookup"><span data-stu-id="053ab-127">In the **search box**, type **SCC LifeCycle**.</span></span>
   
    <span data-ttu-id="053ab-128">![Galerii aplikacji](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "galerii aplikacji")</span><span class="sxs-lookup"><span data-stu-id="053ab-128">![Application Gallery](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Application Gallery")</span></span>
7. <span data-ttu-id="053ab-129">W okienku wyników wybierz **cyklu życia SCC**, a następnie kliknij przycisk **Complete** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="053ab-129">In the results pane, select **SCC LifeCycle**, and then click **Complete** to add the application.</span></span>
   
    <span data-ttu-id="053ab-130">![Cykl życia SCC](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC cykl życia")</span><span class="sxs-lookup"><span data-stu-id="053ab-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="053ab-131">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="053ab-131">Configure single sign-on</span></span>

<span data-ttu-id="053ab-132">Celem tej sekcji jest przedstawiają sposób umożliwić użytkownikom uwierzytelnianie na cyklu życia SCC do swojego konta w usłudze Azure AD przy użyciu federacyjnego na podstawie protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="053ab-132">The objective of this section is to outline how to enable users to authenticate to SCC LifeCycle with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="053ab-133">**Aby skonfigurować rejestrację jednokrotną, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="053ab-133">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="053ab-134">W klasycznym portalu Azure na **cyklu życia SCC** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć ** skonfigurować rejestrację jednokrotną ** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="053ab-134">In the Azure classic portal, on the **SCC LifeCycle** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="053ab-135">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="053ab-135">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="053ab-136">Na **jak chcesz użytkownikom zalogować się na cyklu życia SCC** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="053ab-136">On the **How would you like users to sign on to SCC LifeCycle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="053ab-137">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="053ab-137">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="053ab-138">Na **Konfigurowanie adresu URL aplikacji** strony w **na adres URL logowania** tekstowym, wpisz adres URL używany przez użytkowników do logowania się SCC cyklem życia aplikacji przy użyciu następującego wzorca "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="053ab-138">On the **Configure App URL** page, in the **Sign On URL** textbox, type the URL used by your users to sign on to your SCC LifeCycle application using the following pattern "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", and then click **Next**.</span></span>
   
    <span data-ttu-id="053ab-139">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="053ab-139">![Configure App URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configure App URL")</span></span>
4. <span data-ttu-id="053ab-140">Na **skonfigurować logowanie jednokrotne w cyklu życia SCC** kliknij przycisk **pobierania metadanych**, a następnie zapisz plik metadanych lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="053ab-140">On the **Configure single sign-on at SCC LifeCycle** page, click **Download metadata**, and then save metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="053ab-141">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="053ab-141">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="053ab-142">Przesyła ten plik metadanych, aby SCC cyklu życia z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="053ab-142">Forward that Metadata file to SCC LifeCycle Support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="053ab-143">Logowania jednokrotnego musi zostać włączona przez zespół pomocy technicznej SCC cyklu życia.</span><span class="sxs-lookup"><span data-stu-id="053ab-143">Single sign-on has to be enabled by the SCC LifeCycle support team.</span></span>
   > 
   > 

6. <span data-ttu-id="053ab-144">W klasycznym portalu Azure, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij przycisk **Complete** zamknąć **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="053ab-144">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="053ab-145">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="053ab-145">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="053ab-146">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="053ab-146">Configure user provisioning</span></span>

<span data-ttu-id="053ab-147">Aby włączyć logowanie w cyklu życia SCC użytkowników usługi Azure AD, muszą mieć przydzielone do SCC cyklu życia.</span><span class="sxs-lookup"><span data-stu-id="053ab-147">In order to enable Azure AD users to log into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="053ab-148">Nie ma elementu akcji można skonfigurować do cyklu życia SCC Inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="053ab-148">There is no action item for you to configure user provisioning to SCC LifeCycle.</span></span>

<span data-ttu-id="053ab-149">Gdy przypisany użytkownik próbuje zalogować się na cyklu życia SCC, konto cyklu życia SCC jest tworzony automatycznie w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="053ab-149">When an assigned user tries to log into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="053ab-150">Możesz użyć innych cyklu życia SCC użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez SCC cyklu życia do kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="053ab-150">You can use any other SCC LifeCycle user account creation tools or APIs provided by SCC LifeCycle to provision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="053ab-151">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="053ab-151">Assign users</span></span>
<span data-ttu-id="053ab-152">Aby przetestować konfigurację, musisz przyznać użytkowników usługi Azure AD, czy chcesz zezwolić, używając przypisywania do nich dostęp aplikacji do niego.</span><span class="sxs-lookup"><span data-stu-id="053ab-152">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="053ab-153">**Do przypisywania użytkowników do SCC cyklu życia, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="053ab-153">**To assign users to SCC LifeCycle, perform the following steps:**</span></span>

1. <span data-ttu-id="053ab-154">W klasycznym portalu Azure Utwórz konto testu.</span><span class="sxs-lookup"><span data-stu-id="053ab-154">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="053ab-155">Na ** cyklu życia SCC ** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="053ab-155">On the **SCC LifeCycle **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="053ab-156">![Przypisywanie użytkowników](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "przypisywanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="053ab-156">![Assign Users](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assign Users")</span></span>
3. <span data-ttu-id="053ab-157">Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** o potwierdzenie przypisania.</span><span class="sxs-lookup"><span data-stu-id="053ab-157">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
    <span data-ttu-id="053ab-158">![Tak](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "tak")</span><span class="sxs-lookup"><span data-stu-id="053ab-158">![Yes](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="053ab-159">Jeśli chcesz przetestować ustawienia logowania jednokrotnego, otwórz Panel dostępu.</span><span class="sxs-lookup"><span data-stu-id="053ab-159">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="053ab-160">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="053ab-160">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

