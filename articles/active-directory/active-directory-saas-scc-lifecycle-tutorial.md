---
title: "Samouczek: Azure Active Directory integrację z cyklem życia SCC | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse SCC cyklu życia z usługą Azure Active Directory tooenable pojedynczy logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
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
ms.openlocfilehash: c10c313c5fc157ed70d2ccecfb930a8a765f8444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-scc-lifecycle"></a><span data-ttu-id="cd439-103">Samouczek: Azure Active Directory integrację z cyklem życia SCC</span><span class="sxs-lookup"><span data-stu-id="cd439-103">Tutorial: Azure Active Directory integration with SCC LifeCycle</span></span>
<span data-ttu-id="cd439-104">Celem Hello tego samouczka jest tooshow integracji hello Azure i SCC cyklu życia.</span><span class="sxs-lookup"><span data-stu-id="cd439-104">hello objective of this tutorial is tooshow hello integration of Azure and SCC LifeCycle.</span></span>  

<span data-ttu-id="cd439-105">Scenariusz Hello opisane w tym samouczku założono, że już hello następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="cd439-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="cd439-106">Ważnej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="cd439-106">A valid Azure subscription</span></span>
* <span data-ttu-id="cd439-107">Cykl życia SCC rejestracji jednokrotnej (SSO) włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="cd439-107">A SCC LifeCycle single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="cd439-108">Ten samouczek hello użytkowników usługi Azure AD przypisano tooSCC będzie cyklu życia stanie toosingle logowania do aplikacji hello w witrynie firmy SCC cyklu życia (usługa zainicjował dostawcy logowania) lub przy użyciu hello [wprowadzenie Panel dostępu toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cd439-108">After completing this tutorial, hello Azure AD users you have assigned tooSCC LifeCycle will be able toosingle sign into hello application at your SCC LifeCycle company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="cd439-109">Scenariusz Hello opisane w tym samouczku składa się z powitania po bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="cd439-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="cd439-110">Włączanie integracji aplikacji hello dla SCC cykl życia</span><span class="sxs-lookup"><span data-stu-id="cd439-110">Enabling hello application integration for SCC LifeCycle</span></span>
2. <span data-ttu-id="cd439-111">Konfigurowanie rejestracji jednokrotnej (SSO)</span><span class="sxs-lookup"><span data-stu-id="cd439-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="cd439-112">Konfigurowanie Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="cd439-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="cd439-113">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="cd439-113">Assigning users</span></span>

<span data-ttu-id="cd439-114">![Scenariusz](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "scenariusza")</span><span class="sxs-lookup"><span data-stu-id="cd439-114">![Scenario](./media/active-directory-saas-scc-lifecycle-tutorial/IC794120.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-scc-lifecycle"></a><span data-ttu-id="cd439-115">Włącz integrację aplikacji hello dla SCC cykl życia</span><span class="sxs-lookup"><span data-stu-id="cd439-115">Enable hello application integration for SCC LifeCycle</span></span>
<span data-ttu-id="cd439-116">Celem Hello w tej sekcji jest toooutline sposób integracji aplikacji hello tooenable dla SCC cyklu życia.</span><span class="sxs-lookup"><span data-stu-id="cd439-116">hello objective of this section is toooutline how tooenable hello application integration for SCC LifeCycle.</span></span>

<span data-ttu-id="cd439-117">**Integracja aplikacji hello tooenable dla SCC cykl życia, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="cd439-117">**tooenable hello application integration for SCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd439-118">W hello klasycznego portalu Azure, w okienku nawigacji po lewej stronie powitania kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cd439-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="cd439-119">![Usługi Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "usługi Active Directory")</span><span class="sxs-lookup"><span data-stu-id="cd439-119">![Active Directory](./media/active-directory-saas-scc-lifecycle-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="cd439-120">Z hello **katalogu** listy, wybierz hello katalogu, dla której ma zostać tooenable integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="cd439-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="cd439-121">Kliknij widok aplikacji hello tooopen, w widoku katalogu hello **aplikacji** w menu u góry hello.</span><span class="sxs-lookup"><span data-stu-id="cd439-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="cd439-122">![Aplikacje](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "aplikacji")</span><span class="sxs-lookup"><span data-stu-id="cd439-122">![Applications](./media/active-directory-saas-scc-lifecycle-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="cd439-123">Kliknij przycisk **Dodaj** u dołu hello hello strony.</span><span class="sxs-lookup"><span data-stu-id="cd439-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="cd439-124">![Dodaj aplikację](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Dodaj aplikację")</span><span class="sxs-lookup"><span data-stu-id="cd439-124">![Add application](./media/active-directory-saas-scc-lifecycle-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="cd439-125">Na powitania **co chcesz toodo** okna dialogowego, kliknij przycisk **dodać aplikację z galerii hello**.</span><span class="sxs-lookup"><span data-stu-id="cd439-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="cd439-126">![Dodawanie aplikacji z gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "dodać aplikację z gallerry")</span><span class="sxs-lookup"><span data-stu-id="cd439-126">![Add an application from gallerry](./media/active-directory-saas-scc-lifecycle-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="cd439-127">W hello **pole wyszukiwania**, typ **cyklu życia SCC**.</span><span class="sxs-lookup"><span data-stu-id="cd439-127">In hello **search box**, type **SCC LifeCycle**.</span></span>
   
    <span data-ttu-id="cd439-128">![Galerii aplikacji](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "galerii aplikacji")</span><span class="sxs-lookup"><span data-stu-id="cd439-128">![Application Gallery](./media/active-directory-saas-scc-lifecycle-tutorial/IC794121.png "Application Gallery")</span></span>
7. <span data-ttu-id="cd439-129">W okienku wyników hello, wybierz **cyklu życia SCC**, a następnie kliknij przycisk **Complete** aplikacji hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="cd439-129">In hello results pane, select **SCC LifeCycle**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="cd439-130">![Cykl życia SCC](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC cykl życia")</span><span class="sxs-lookup"><span data-stu-id="cd439-130">![SCC LifeCycle](./media/active-directory-saas-scc-lifecycle-tutorial/IC795082.png "SCC LifeCycle")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="cd439-131">Konfigurowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="cd439-131">Configure single sign-on</span></span>

<span data-ttu-id="cd439-132">Celem Hello w tej sekcji jest toooutline jak tooenable użytkowników tooauthenticate tooSCC cyklu życia do swojego konta w usłudze Azure AD przy użyciu Federacji oparte na powitania protokołu SAML.</span><span class="sxs-lookup"><span data-stu-id="cd439-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooSCC LifeCycle with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="cd439-133">**tooconfigure logowanie jednokrotne, wykonaj następujące kroki hello:**</span><span class="sxs-lookup"><span data-stu-id="cd439-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd439-134">W hello klasycznego portalu Azure na powitania **cyklu życia SCC** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** tooopen hello ** skonfigurować rejestrację jednokrotną ** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cd439-134">In hello Azure classic portal, on hello **SCC LifeCycle** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="cd439-135">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cd439-135">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794122.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="cd439-136">Na powitania **jak ma toosign użytkowników na tooSCC cyklu życia** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="cd439-136">On hello **How would you like users toosign on tooSCC LifeCycle** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="cd439-137">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cd439-137">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794123.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="cd439-138">Na powitania **Konfigurowanie adresu URL aplikacji** strony w hello **na adres URL logowania** pole tekstowe, wprowadź adres URL hello używany przez Twoje toosign użytkowników na tooyour SCC cyklem życia aplikacji przy użyciu następującego wzorca hello "*https:// bs1.SCC.com/lc7/Welcome/Customer/PICTtest.aspx*", a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="cd439-138">On hello **Configure App URL** page, in hello **Sign On URL** textbox, type hello URL used by your users toosign on tooyour SCC LifeCycle application using hello following pattern "*https://bs1.scc.com/lc7/welcome/customer/PICTtest.aspx*", and then click **Next**.</span></span>
   
    <span data-ttu-id="cd439-139">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="cd439-139">![Configure App URL](./media/active-directory-saas-scc-lifecycle-tutorial/IC794124.png "Configure App URL")</span></span>
4. <span data-ttu-id="cd439-140">Na powitania **skonfigurować logowanie jednokrotne w cyklu życia SCC** kliknij przycisk **pobierania metadanych**, a następnie zapisz plik metadanych lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="cd439-140">On hello **Configure single sign-on at SCC LifeCycle** page, click **Download metadata**, and then save metadata file locally on your computer.</span></span>
   
   <span data-ttu-id="cd439-141">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cd439-141">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC795083.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="cd439-142">Przesyła tego tooSCC pliku metadanych cyklu życia z pomocą techniczną.</span><span class="sxs-lookup"><span data-stu-id="cd439-142">Forward that Metadata file tooSCC LifeCycle Support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="cd439-143">Logowanie jednokrotne ma toobe włączane przez hello cyklu życia SCC zespołem pomocy technicznej.</span><span class="sxs-lookup"><span data-stu-id="cd439-143">Single sign-on has toobe enabled by hello SCC LifeCycle support team.</span></span>
   > 
   > 

6. <span data-ttu-id="cd439-144">Na powitania klasycznego portalu Azure, wybierz hello konfiguracji rejestracji jednokrotnej potwierdzenie, a następnie kliknij **Complete** tooclose hello **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cd439-144">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="cd439-145">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="cd439-145">![Configure Single Sign-On](./media/active-directory-saas-scc-lifecycle-tutorial/IC794125.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="cd439-146">Skonfiguruj Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="cd439-146">Configure user provisioning</span></span>

<span data-ttu-id="cd439-147">W przypadku użytkowników usługi Azure AD toolog kolejności tooenable w cyklu życia SCC muszą mieć przydzielone do SCC cyklu życia.</span><span class="sxs-lookup"><span data-stu-id="cd439-147">In order tooenable Azure AD users toolog into SCC LifeCycle, they must be provisioned into SCC LifeCycle.</span></span> <span data-ttu-id="cd439-148">Nie ma elementu akcji można tooconfigure użytkownika inicjowania obsługi administracyjnej tooSCC cyklu życia.</span><span class="sxs-lookup"><span data-stu-id="cd439-148">There is no action item for you tooconfigure user provisioning tooSCC LifeCycle.</span></span>

<span data-ttu-id="cd439-149">Gdy toolog prób przypisany użytkownik w cyklu życia SCC konta cyklu życia SCC jest tworzony automatycznie w razie potrzeby.</span><span class="sxs-lookup"><span data-stu-id="cd439-149">When an assigned user tries toolog into SCC LifeCycle, an SCC LifeCycle account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="cd439-150">Możesz użyć innych cyklu życia SCC użytkownika konta tworzenia narzędzi lub interfejsów API dostarczonych przez SCC cyklu życia tooprovision kont użytkowników usługi AAD.</span><span class="sxs-lookup"><span data-stu-id="cd439-150">You can use any other SCC LifeCycle user account creation tools or APIs provided by SCC LifeCycle tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="cd439-151">Przypisywanie użytkowników</span><span class="sxs-lookup"><span data-stu-id="cd439-151">Assign users</span></span>
<span data-ttu-id="cd439-152">tootest konfiguracji, należy toogrant hello Azure AD użytkownicy mają tooallow przy użyciu Twojej aplikacji tooit dostępu przez przypisywanie ich.</span><span class="sxs-lookup"><span data-stu-id="cd439-152">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="cd439-153">**tooassign użytkowników tooSCC cykl życia, wykonaj hello następujące kroki:**</span><span class="sxs-lookup"><span data-stu-id="cd439-153">**tooassign users tooSCC LifeCycle, perform hello following steps:**</span></span>

1. <span data-ttu-id="cd439-154">W hello klasycznego portalu Azure Utwórz konto testu.</span><span class="sxs-lookup"><span data-stu-id="cd439-154">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="cd439-155">Na powitania ** cyklu życia SCC ** strona integracji aplikacji, kliknij przycisk **przypisywać użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="cd439-155">On hello **SCC LifeCycle **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="cd439-156">![Przypisywanie użytkowników](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "przypisywanie użytkowników")</span><span class="sxs-lookup"><span data-stu-id="cd439-156">![Assign Users](./media/active-directory-saas-scc-lifecycle-tutorial/IC794126.png "Assign Users")</span></span>
3. <span data-ttu-id="cd439-157">Wybierz użytkownika testowego, kliknij przycisk **przypisać**, a następnie kliknij przycisk **tak** tooconfirm przypisania.</span><span class="sxs-lookup"><span data-stu-id="cd439-157">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="cd439-158">![Tak](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "tak")</span><span class="sxs-lookup"><span data-stu-id="cd439-158">![Yes](./media/active-directory-saas-scc-lifecycle-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="cd439-159">Jeśli chcesz tootest ustawienia logowania jednokrotnego, otwórz hello panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="cd439-159">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="cd439-160">Aby uzyskać więcej informacji na temat hello Panel dostępu, zobacz [toohello wprowadzenie panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cd439-160">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

