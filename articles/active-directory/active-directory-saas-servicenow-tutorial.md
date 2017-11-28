---
title: "Samouczek: Integracji Azure Active Directory z usługi ServiceNow | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i usługi ServiceNow i usługi ServiceNow Express."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 1d8eb99e-8ce5-4ba4-8b54-5c3d9ae573f6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: a91fab90a94b655b93c8ae9064ea4836b80d7678
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicenow"></a><span data-ttu-id="5249c-103">Samouczek: Integracji Azure Active Directory z usługi ServiceNow</span><span class="sxs-lookup"><span data-stu-id="5249c-103">Tutorial: Azure Active Directory integration with ServiceNow</span></span>
<span data-ttu-id="5249c-104">Z tego samouczka dowiesz się Integrowanie usługi ServiceNow i Express usługi ServiceNow z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5249c-104">In this tutorial, you learn how to integrate ServiceNow and ServiceNow Express with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5249c-105">Integrowanie usługi ServiceNow i Express usługi ServiceNow z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="5249c-105">Integrating ServiceNow and ServiceNow Express with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="5249c-106">Można kontrolować w usłudze Azure AD, kto ma dostęp do usługi ServiceNow oraz usługi ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="5249c-106">You can control in Azure AD who has access to ServiceNow and ServiceNow Express</span></span>
* <span data-ttu-id="5249c-107">Umożliwia użytkownikom automatycznie pobrać zalogowane usługi ServiceNow i usługi ServiceNow Express (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5249c-107">You can enable your users to automatically get signed-on to ServiceNow and ServiceNow Express (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="5249c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="5249c-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="5249c-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5249c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5249c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="5249c-110">Prerequisites</span></span>
<span data-ttu-id="5249c-111">Aby skonfigurować integrację usługi Azure AD z usługi ServiceNow i Express usługi ServiceNow, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="5249c-111">To configure Azure AD integration with ServiceNow and ServiceNow Express, you need the following items:</span></span>

* <span data-ttu-id="5249c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5249c-112">An Azure AD subscription</span></span>
* <span data-ttu-id="5249c-113">Dla usługi ServiceNow, wystąpienie lub dzierżawy usługi ServiceNow, wersja Calgary lub nowszej</span><span class="sxs-lookup"><span data-stu-id="5249c-113">For ServiceNow, an instance or tenant of ServiceNow, Calgary version or higher</span></span>
* <span data-ttu-id="5249c-114">Usługi ServiceNow Express, wystąpienie usługi ServiceNow Express, wersja Helsinkach lub nowszej</span><span class="sxs-lookup"><span data-stu-id="5249c-114">For ServiceNow Express, an instance of ServiceNow Express, Helsinki version or higher</span></span>
* <span data-ttu-id="5249c-115">Dzierżawca usługi ServiceNow musi mieć [wielu pojedynczy znak na dodatek dostawcy](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) włączone.</span><span class="sxs-lookup"><span data-stu-id="5249c-115">The ServiceNow tenant must have the [Multiple Provider Single Sign On Plugin](http://wiki.servicenow.com/index.php?title=Multiple_Provider_Single_Sign-On#gsc.tab=0) enabled.</span></span> <span data-ttu-id="5249c-116">Można to zrobić [przesyłanie żądania obsługi](https://hi.service-now.com).</span><span class="sxs-lookup"><span data-stu-id="5249c-116">This can be done by [submitting a service request](https://hi.service-now.com).</span></span> 

> [!NOTE]
> <span data-ttu-id="5249c-117">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="5249c-117">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="5249c-118">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="5249c-118">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="5249c-119">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="5249c-119">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="5249c-120">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5249c-120">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5249c-121">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="5249c-121">Scenario description</span></span>
<span data-ttu-id="5249c-122">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="5249c-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5249c-123">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="5249c-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5249c-124">Dodawanie usługi ServiceNow z galerii</span><span class="sxs-lookup"><span data-stu-id="5249c-124">Adding ServiceNow from the gallery</span></span>
2. <span data-ttu-id="5249c-125">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne dla usługi ServiceNow lub usługi ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="5249c-125">Configuring and testing Azure AD single sign-on for ServiceNow or ServiceNow Express</span></span>

## <a name="adding-servicenow-from-the-gallery"></a><span data-ttu-id="5249c-126">Dodawanie usługi ServiceNow z galerii</span><span class="sxs-lookup"><span data-stu-id="5249c-126">Adding ServiceNow from the gallery</span></span>
<span data-ttu-id="5249c-127">Aby skonfigurować integrację usługi ServiceNow lub Express usługi ServiceNow z usługą Azure AD, należy dodać usługi ServiceNow z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="5249c-127">To configure the integration of ServiceNow or ServiceNow Express into Azure AD, you need to add ServiceNow from the gallery to your list of managed SaaS apps.</span></span> 

<span data-ttu-id="5249c-128">**Aby dodać usługi ServiceNow z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5249c-128">**To add ServiceNow from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5249c-129">W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5249c-129">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Usługa Active Directory][1]
2. <span data-ttu-id="5249c-131">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="5249c-131">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="5249c-132">Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="5249c-132">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Aplikacje][2]
4. <span data-ttu-id="5249c-134">Kliknij przycisk **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="5249c-134">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplikacje][3]
5. <span data-ttu-id="5249c-136">Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.</span><span class="sxs-lookup"><span data-stu-id="5249c-136">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Aplikacje][4]
6. <span data-ttu-id="5249c-138">W polu wyszukiwania wpisz **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="5249c-138">In the search box, type **ServiceNow**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_01.png)
7. <span data-ttu-id="5249c-140">W okienku wyników wybierz **ServiceNow**, a następnie kliknij przycisk **Complete** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="5249c-140">In the results pane, select **ServiceNow**, and then click **Complete** to add the application.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_02.png)

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5249c-142">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="5249c-142">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5249c-143">W tej sekcji możesz skonfigurować i test usługi Azure AD rejestracji jednokrotnej z usługi ServiceNow lub Express usługi ServiceNow w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="5249c-143">In this section, you configure and test Azure AD single sign-on with ServiceNow or ServiceNow Express based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5249c-144">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w ServiceNow jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5249c-144">For single sign-on to work, Azure AD needs to know what the counterpart user in ServiceNow is to a user in Azure AD.</span></span> <span data-ttu-id="5249c-145">Innymi słowy łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w usługi ServiceNow musi się.</span><span class="sxs-lookup"><span data-stu-id="5249c-145">In other words, a link relationship between an Azure AD user and the related user in ServiceNow needs to be established.</span></span>
<span data-ttu-id="5249c-146">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="5249c-146">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ServiceNow.</span></span> <span data-ttu-id="5249c-147">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z usługi ServiceNow, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="5249c-147">To configure and test Azure AD single sign-on with ServiceNow, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5249c-148">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej dla usługi ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5249c-148">**[Configuring Azure AD Single Sign-On for ServiceNow](#configuring-azure-ad-single-sign-on-for-servicenow)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5249c-149">**[Konfigurowanie usługi Azure AD logowania jednokrotnego usługi ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="5249c-149">**[Configuring Azure AD Single Sign-On for ServiceNow Express](#configuring-azure-ad-single-sign-on-for-servicenow-express)** - to enable your users to use this feature.</span></span>
3. <span data-ttu-id="5249c-150">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5249c-150">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="5249c-151">**[Tworzenie użytkownika testowego usługi ServiceNow](#creating-a-servicenow-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta ServiceNow połączonego z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5249c-151">**[Creating a ServiceNow test user](#creating-a-servicenow-test-user)** - to have a counterpart of Britta Simon in ServiceNow that is linked to the Azure AD representation of her.</span></span>
5. <span data-ttu-id="5249c-152">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5249c-152">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="5249c-153">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="5249c-153">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

> [!NOTE]
> <span data-ttu-id="5249c-154">Jeśli chcesz skonfigurować usługi ServiceNow pominąć krok 2.</span><span class="sxs-lookup"><span data-stu-id="5249c-154">If you want to configure ServiceNow omit step 2.</span></span> <span data-ttu-id="5249c-155">Podobnie jeśli chcesz skonfigurować usługi ServiceNow Express pominąć krok 1.</span><span class="sxs-lookup"><span data-stu-id="5249c-155">Likewise, if you want to configure ServiceNow Express omit step 1.</span></span>
> 
> 

### <a name="configuring-azure-ad-single-sign-on-for-servicenow"></a><span data-ttu-id="5249c-156">Konfigurowanie usługi Azure AD rejestracji jednokrotnej dla usługi ServiceNow</span><span class="sxs-lookup"><span data-stu-id="5249c-156">Configuring Azure AD Single Sign-On for ServiceNow</span></span>
1. <span data-ttu-id="5249c-157">W klasycznym portalu usługi Azure AD na **ServiceNow** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5249c-157">In the Azure AD classic portal, on the **ServiceNow** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="5249c-158">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC749323.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-158">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="5249c-159">Na **jak chcesz użytkownikom zalogować się do usługi ServiceNow** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="5249c-159">On the **How would you like users to sign on to ServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="5249c-160">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC749324.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-160">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="5249c-161">Na **Konfigurowanie ustawień aplikacji** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5249c-161">On the **Configure App Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="5249c-162">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/IC769497.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="5249c-162">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="5249c-163">a.</span><span class="sxs-lookup"><span data-stu-id="5249c-163">a.</span></span> <span data-ttu-id="5249c-164">w **usługi ServiceNow na adres URL logowania** tekstowym, wpisz adres URL używany przez użytkowników do logowania jednokrotnego do aplikacji usługi ServiceNow zgodnie ze wzorcem: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="5249c-164">in the **ServiceNow Sign On URL** textbox, type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="5249c-165">b.</span><span class="sxs-lookup"><span data-stu-id="5249c-165">b.</span></span> <span data-ttu-id="5249c-166">W **identyfikator** tekstowym, wpisz adres URL używany przez użytkowników do logowania jednokrotnego do aplikacji usługi ServiceNow zgodnie ze wzorcem: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="5249c-166">In the **Identifier** textbox,type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="5249c-167">c.</span><span class="sxs-lookup"><span data-stu-id="5249c-167">c.</span></span> <span data-ttu-id="5249c-168">Kliknij przycisk **Dalej**</span><span class="sxs-lookup"><span data-stu-id="5249c-168">Click **Next**</span></span>

4. <span data-ttu-id="5249c-169">Aby program Azure AD automatycznie konfigurować usługi ServiceNow dla uwierzytelniania opartego na SAML, wprowadź Twojej nazwy wystąpienia usługi ServiceNow, nazwa użytkownika i hasło administratora w **automatycznie skonfigurować logowanie jednokrotne** tworzą, a następnie kliknij przycisk  *Skonfiguruj*.</span><span class="sxs-lookup"><span data-stu-id="5249c-169">To have Azure AD automatically configure ServiceNow for SAML-based authentication, enter your ServiceNow instance name, admin username, and admin password in the **Auto configure single sign-on** form and click *Configure*.</span></span> <span data-ttu-id="5249c-170">Należy pamiętać, że podana nazwa użytkownika administratora musi mieć **security_admin** rola przypisana w usługi ServiceNow tej pracy.</span><span class="sxs-lookup"><span data-stu-id="5249c-170">Note that the admin username provided must have the **security_admin** role assigned in ServiceNow for this to work.</span></span> <span data-ttu-id="5249c-171">W przeciwnym razie, aby ręcznie skonfigurować usługi ServiceNow przy użyciu usługi Azure AD jako dostawca tożsamości SAML, kliknij przycisk **ręcznie skonfigurować aplikację do logowania jednokrotnego**, następnie kliknij przycisk **dalej** i wykonaj następujące czynności .</span><span class="sxs-lookup"><span data-stu-id="5249c-171">Otherwise, to manually configure ServiceNow to use Azure AD as a SAML identity provider, click **Manually configure the application for single sign-on**, then click **Next** and complete the following steps.</span></span>
   
    <span data-ttu-id="5249c-172">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="5249c-172">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="5249c-173">Na **skonfigurować logowanie jednokrotne w ServiceNow** kliknij przycisk **pobierania certyfikatu**, Zapisz plik certyfikatu lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="5249c-173">On the **Configure single sign-on at ServiceNow** page, click **Download certificate**, save the certificate file locally on your computer.</span></span>
   
    <span data-ttu-id="5249c-174">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC749325.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-174">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="5249c-175">Logowanie do aplikacji usługi ServiceNow jako administrator.</span><span class="sxs-lookup"><span data-stu-id="5249c-175">Sign-on to your ServiceNow application as an administrator.</span></span>

7. <span data-ttu-id="5249c-176">Aktywuj *integracja — wiele pojedynczego logowania Instalatora dostawcy* wtyczki dalej wykonaj czynności:</span><span class="sxs-lookup"><span data-stu-id="5249c-176">Activate the *Integration - Multiple Provider Single Sign-On Installer* plugin by following the next steps:</span></span>
   
    <span data-ttu-id="5249c-177">a.</span><span class="sxs-lookup"><span data-stu-id="5249c-177">a.</span></span> <span data-ttu-id="5249c-178">W okienku nawigacji po lewej stronie, przejdź do **definicji systemu** sekcji, a następnie kliknij przycisk **wtyczek**.</span><span class="sxs-lookup"><span data-stu-id="5249c-178">In the navigation pane on the left side, go to **System Definition** section and then click **Plugins**.</span></span>
   
    <span data-ttu-id="5249c-179">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "aktywowanie wtyczki")</span><span class="sxs-lookup"><span data-stu-id="5249c-179">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_03.png "Activate plugin")</span></span>
   
    <span data-ttu-id="5249c-180">b.</span><span class="sxs-lookup"><span data-stu-id="5249c-180">b.</span></span> <span data-ttu-id="5249c-181">Wyszukaj *integracja — wiele pojedynczego logowania Instalatora dostawcy*.</span><span class="sxs-lookup"><span data-stu-id="5249c-181">Search for *Integration - Multiple Provider Single Sign-On Installer*.</span></span>
   
    <span data-ttu-id="5249c-182">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "aktywowanie wtyczki")</span><span class="sxs-lookup"><span data-stu-id="5249c-182">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_04.png "Activate plugin")</span></span>
   
    <span data-ttu-id="5249c-183">c.</span><span class="sxs-lookup"><span data-stu-id="5249c-183">c.</span></span> <span data-ttu-id="5249c-184">Wybierz wtyczki.</span><span class="sxs-lookup"><span data-stu-id="5249c-184">Select the plugin.</span></span> <span data-ttu-id="5249c-185">Rigth kliknij i zaznacz **Aktywuj/Upgrade**.</span><span class="sxs-lookup"><span data-stu-id="5249c-185">Rigth click and select **Activate/Upgrade**.</span></span>
   
    <span data-ttu-id="5249c-186">d.</span><span class="sxs-lookup"><span data-stu-id="5249c-186">d.</span></span> <span data-ttu-id="5249c-187">Kliknij przycisk **Aktywuj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="5249c-187">Click the **Activate** button.</span></span>

8. <span data-ttu-id="5249c-188">W okienku nawigacji po lewej stronie kliknij **właściwości**.</span><span class="sxs-lookup"><span data-stu-id="5249c-188">In the navigation pane on the left side, click **Properties**.</span></span>  
   
    <span data-ttu-id="5249c-189">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="5249c-189">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_06.png "Configure app URL")</span></span>

9. <span data-ttu-id="5249c-190">Na **wiele właściwości logowania jednokrotnego dostawcy** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5249c-190">On the **Multiple Provider SSO Properties** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="5249c-191">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="5249c-191">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694981.png "Configure app URL")</span></span>
   
    <span data-ttu-id="5249c-192">a.</span><span class="sxs-lookup"><span data-stu-id="5249c-192">a.</span></span> <span data-ttu-id="5249c-193">Jako **włączyć wiele dostawcy logowania jednokrotnego**, wybierz pozycję **tak**.</span><span class="sxs-lookup"><span data-stu-id="5249c-193">As **Enable multiple provider SSO**, select **Yes**.</span></span>
   
    <span data-ttu-id="5249c-194">b.</span><span class="sxs-lookup"><span data-stu-id="5249c-194">b.</span></span> <span data-ttu-id="5249c-195">Jako **włączania rejestrowania debugowania uzyskano wiele dostawcy logowania jednokrotnego integracji**, wybierz pozycję **tak**.</span><span class="sxs-lookup"><span data-stu-id="5249c-195">As **Enable debug logging got the multiple provider SSO integration**, select **Yes**.</span></span>
   
    <span data-ttu-id="5249c-196">c.</span><span class="sxs-lookup"><span data-stu-id="5249c-196">c.</span></span> <span data-ttu-id="5249c-197">W **tabeli pole użytkownika, który...**  pole tekstowe, typ **nazwa_użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="5249c-197">In **The field on the user table that...** textbox, type **user_name**.</span></span>
   
    <span data-ttu-id="5249c-198">d.</span><span class="sxs-lookup"><span data-stu-id="5249c-198">d.</span></span> <span data-ttu-id="5249c-199">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="5249c-199">Click **Save**.</span></span>

10. <span data-ttu-id="5249c-200">W okienku nawigacji po lewej stronie kliknij **certyfikaty x509**.</span><span class="sxs-lookup"><span data-stu-id="5249c-200">In the navigation pane on the left side, click **x509 Certificates**.</span></span>
    
     <span data-ttu-id="5249c-201">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-201">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_05.png "Configure single sign-on")</span></span>

11. <span data-ttu-id="5249c-202">Na **certyfikatów X.509** okna dialogowego, kliknij przycisk **nowy**.</span><span class="sxs-lookup"><span data-stu-id="5249c-202">On the **X.509 Certificates** dialog, click **New**.</span></span>
    
     <span data-ttu-id="5249c-203">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-203">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694974.png "Configure single sign-on")</span></span>

12. <span data-ttu-id="5249c-204">Na **certyfikatów X.509** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5249c-204">On the **X.509 Certificates** dialog, perform the following steps:</span></span>
    
     <span data-ttu-id="5249c-205">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-205">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
     <span data-ttu-id="5249c-206">a.</span><span class="sxs-lookup"><span data-stu-id="5249c-206">a.</span></span> <span data-ttu-id="5249c-207">Kliknij przycisk **Nowy**.</span><span class="sxs-lookup"><span data-stu-id="5249c-207">Click **New**.</span></span>
    
     <span data-ttu-id="5249c-208">b.</span><span class="sxs-lookup"><span data-stu-id="5249c-208">b.</span></span> <span data-ttu-id="5249c-209">W **nazwa** tekstowym, wpisz nazwę konfiguracji (np.: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="5249c-209">In the **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
     <span data-ttu-id="5249c-210">c.</span><span class="sxs-lookup"><span data-stu-id="5249c-210">c.</span></span> <span data-ttu-id="5249c-211">Wybierz **Active**.</span><span class="sxs-lookup"><span data-stu-id="5249c-211">Select **Active**.</span></span>
    
     <span data-ttu-id="5249c-212">d.</span><span class="sxs-lookup"><span data-stu-id="5249c-212">d.</span></span> <span data-ttu-id="5249c-213">Jako **Format**, wybierz pozycję **PEM**.</span><span class="sxs-lookup"><span data-stu-id="5249c-213">As **Format**, select **PEM**.</span></span>
    
     <span data-ttu-id="5249c-214">e.</span><span class="sxs-lookup"><span data-stu-id="5249c-214">e.</span></span> <span data-ttu-id="5249c-215">Jako **typu**, wybierz pozycję **zaufania certyfikatów magazynu**.</span><span class="sxs-lookup"><span data-stu-id="5249c-215">As **Type**, select **Trust Store Cert**.</span></span>
    
     <span data-ttu-id="5249c-216">f.</span><span class="sxs-lookup"><span data-stu-id="5249c-216">f.</span></span> <span data-ttu-id="5249c-217">Otwórz w Notatniku Twojego certyfikatu szyfrowania Base64, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikatu PEM** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5249c-217">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span></span>
    
     <span data-ttu-id="5249c-218">g.</span><span class="sxs-lookup"><span data-stu-id="5249c-218">g.</span></span> <span data-ttu-id="5249c-219">Kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="5249c-219">Click **Update**.</span></span>

13. <span data-ttu-id="5249c-220">W okienku nawigacji po lewej stronie kliknij **dostawców tożsamości**.</span><span class="sxs-lookup"><span data-stu-id="5249c-220">In the navigation pane on the left side, click **Identity Providers**.</span></span>
    
     <span data-ttu-id="5249c-221">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-221">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_07.png "Configure single sign-on")</span></span>

14. <span data-ttu-id="5249c-222">Na **dostawców tożsamości** okna dialogowego, kliknij przycisk **nowy**:</span><span class="sxs-lookup"><span data-stu-id="5249c-222">On the **Identity Providers** dialog, click **New**:</span></span>
    
     <span data-ttu-id="5249c-223">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-223">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694977.png "Configure single sign-on")</span></span>

15. <span data-ttu-id="5249c-224">Na **dostawców tożsamości** okna dialogowego, kliknij przycisk **aktualizację1 SAML2?**:</span><span class="sxs-lookup"><span data-stu-id="5249c-224">On the **Identity Providers** dialog, click **SAML2 Update1?**:</span></span>
    
     <span data-ttu-id="5249c-225">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-225">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694978.png "Configure single sign-on")</span></span>

16. <span data-ttu-id="5249c-226">W oknie dialogowym właściwości aktualizację1 SAML2 wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5249c-226">On the SAML2 Update1 Properties dialog, perform the following steps:</span></span>
    
     <span data-ttu-id="5249c-227">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-227">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694982.png "Configure single sign-on")</span></span>

    <span data-ttu-id="5249c-228">a.</span><span class="sxs-lookup"><span data-stu-id="5249c-228">a.</span></span> <span data-ttu-id="5249c-229">w **nazwa** tekstowym, wpisz nazwę konfiguracji (np.: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="5249c-229">in the **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="5249c-230">b.</span><span class="sxs-lookup"><span data-stu-id="5249c-230">b.</span></span> <span data-ttu-id="5249c-231">W **pole użytkownika** pole tekstowe, typ **e-mail** lub **nazwa_użytkownika**, w zależności od pole, które jest używane do unikatowego identyfikowania użytkowników w danym wdrożeniu usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="5249c-231">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="5249c-232">Można configue usługi Azure AD, aby emitować identyfikator użytkownika usługi Azure AD (główna nazwa użytkownika) lub adres e-mail jako unikatowy identyfikator w tokenie SAML, przechodząc do **ServiceNow > atrybuty > logowanie jednokrotne** sekcji klasyczny Portal Azure Portal i mapowanie odpowiednie pola **nameidentifier** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="5249c-232">You can configue Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure classic portal and mapping the desired field to the **nameidentifier** attribute.</span></span> <span data-ttu-id="5249c-233">Wartość przechowywana wybranego atrybutu w usłudze Azure AD (np. główna nazwa użytkownika) musi odpowiadać wartości przechowywane w usługi ServiceNow wprowadzony w polu (np. nazwa_użytkownika)</span><span class="sxs-lookup"><span data-stu-id="5249c-233">The value stored for the selected attribute in Azure AD (e.g. user principal name) must match the value stored in ServiceNow for the entered field (e.g. user_name)</span></span>

    <span data-ttu-id="5249c-234">c.</span><span class="sxs-lookup"><span data-stu-id="5249c-234">c.</span></span> <span data-ttu-id="5249c-235">W klasycznym portalu usługi Azure AD, skopiuj **identyfikator dostawcy tożsamości** wartość, a następnie wklej ją do **adres URL dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5249c-235">In the Azure AD classic portal, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="5249c-236">d.</span><span class="sxs-lookup"><span data-stu-id="5249c-236">d.</span></span> <span data-ttu-id="5249c-237">W klasycznym portalu usługi Azure AD, skopiuj **adres URL żądania uwierzytelniania** wartość, a następnie wklej ją do **AuthnRequest dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5249c-237">In the Azure AD classic portal, copy the **Authentication Request URL** value, and then paste it into the **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="5249c-238">e.</span><span class="sxs-lookup"><span data-stu-id="5249c-238">e.</span></span> <span data-ttu-id="5249c-239">W klasycznym portalu usługi Azure AD, skopiuj **pojedynczy adres URL usługi Sign-Out** wartość, a następnie wklej ją do **SingleLogoutRequest dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5249c-239">In the Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="5249c-240">f.</span><span class="sxs-lookup"><span data-stu-id="5249c-240">f.</span></span> <span data-ttu-id="5249c-241">W **strony głównej usługi ServiceNow** tekstowym, wpisz adres URL strony głównej wystąpienia usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="5249c-241">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5249c-242">Na stronie głównej wystąpienia usługi ServiceNow jest złączeniem Twojej **adres URL dzierżawy ServieNow** i **/navpage.do** (np.:`https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="5249c-242">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.:`https://fabrikam.service-now.com/navpage.do`).</span></span>

    <span data-ttu-id="5249c-243">g.</span><span class="sxs-lookup"><span data-stu-id="5249c-243">g.</span></span> <span data-ttu-id="5249c-244">W **identyfikator podmiot / wystawca** pole tekstowe, wpisz adres URL dzierżawy usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="5249c-244">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span></span>

    <span data-ttu-id="5249c-245">h.</span><span class="sxs-lookup"><span data-stu-id="5249c-245">h.</span></span> <span data-ttu-id="5249c-246">W **URL odbiorców** tekstowym, wpisz adres URL dzierżawy usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="5249c-246">In the **Audience URL** textbox, type the URL of your ServiceNow tenant.</span></span> 

    <span data-ttu-id="5249c-247">i.</span><span class="sxs-lookup"><span data-stu-id="5249c-247">i.</span></span> <span data-ttu-id="5249c-248">W **powiązanie protokołu IDP SingleLogoutRequest** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:2.0:bindings:HTTP-przekierowania**.</span><span class="sxs-lookup"><span data-stu-id="5249c-248">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>

    <span data-ttu-id="5249c-249">j.</span><span class="sxs-lookup"><span data-stu-id="5249c-249">j.</span></span> <span data-ttu-id="5249c-250">W polu tekstowym zasad NameID wpisz **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: nieokreślony**.</span><span class="sxs-lookup"><span data-stu-id="5249c-250">In the NameID Policy textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>

    <span data-ttu-id="5249c-251">k.</span><span class="sxs-lookup"><span data-stu-id="5249c-251">k.</span></span> <span data-ttu-id="5249c-252">Anuluj wybór **utworzyć AuthnContextClass**.</span><span class="sxs-lookup"><span data-stu-id="5249c-252">Deselect **Create an AuthnContextClass**.</span></span>

    <span data-ttu-id="5249c-253">l.</span><span class="sxs-lookup"><span data-stu-id="5249c-253">l.</span></span> <span data-ttu-id="5249c-254">W **metody AuthnContextClassRef**, typ `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span><span class="sxs-lookup"><span data-stu-id="5249c-254">In the **AuthnContextClassRef Method**, type `http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password`.</span></span> <span data-ttu-id="5249c-255">Jest to potrzebne tylko w przypadku organizacji tylko w chmurze.</span><span class="sxs-lookup"><span data-stu-id="5249c-255">This is only needed if you are cloud only organization.</span></span> <span data-ttu-id="5249c-256">Jeśli używasz lokalnych usług AD FS lub usługę MFA dla uwierzytelniania, a następnie ta wartość nie należy konfigurować.</span><span class="sxs-lookup"><span data-stu-id="5249c-256">If you are using on-premises ADFS or MFA for authentication then you should not configure this value.</span></span> 

    <span data-ttu-id="5249c-257">m.</span><span class="sxs-lookup"><span data-stu-id="5249c-257">m.</span></span> <span data-ttu-id="5249c-258">W **pochylanie zegara** pole tekstowe, typ **60**.</span><span class="sxs-lookup"><span data-stu-id="5249c-258">In **Clock Skew** textbox, type **60**.</span></span>

    <span data-ttu-id="5249c-259">n.</span><span class="sxs-lookup"><span data-stu-id="5249c-259">n.</span></span> <span data-ttu-id="5249c-260">Jako **pojedynczy znak na skrypt**, wybierz pozycję **MultiSSO_SAML2_Update1**.</span><span class="sxs-lookup"><span data-stu-id="5249c-260">As **Single Sign On Script**, select **MultiSSO_SAML2_Update1**.</span></span>

    <span data-ttu-id="5249c-261">o.</span><span class="sxs-lookup"><span data-stu-id="5249c-261">o.</span></span> <span data-ttu-id="5249c-262">Jako **x509 certyfikatu**, wybierz certyfikat został utworzony w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="5249c-262">As **x509 Certificate**, select the certificate you have created in the previous step.</span></span>

    <span data-ttu-id="5249c-263">p.</span><span class="sxs-lookup"><span data-stu-id="5249c-263">p.</span></span> <span data-ttu-id="5249c-264">Kliknij przycisk **przesłać**.</span><span class="sxs-lookup"><span data-stu-id="5249c-264">Click **Submit**.</span></span> 

1. <span data-ttu-id="5249c-265">W klasycznym portalu usługi Azure AD, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="5249c-265">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="5249c-266">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-266">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="5249c-267">Na **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="5249c-267">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="5249c-268">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-268">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

### <a name="configuring-azure-ad-single-sign-on-for-servicenow-express"></a><span data-ttu-id="5249c-269">Konfigurowanie usługi Azure AD jednokrotnej usługi ServiceNow Express</span><span class="sxs-lookup"><span data-stu-id="5249c-269">Configuring Azure AD Single Sign-On for ServiceNow Express</span></span>
1. <span data-ttu-id="5249c-270">W klasycznym portalu usługi Azure AD na **ServiceNow** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="5249c-270">In the Azure AD classic portal, on the **ServiceNow** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="5249c-271">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC749323.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-271">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749323.png "Configure single sign-on")</span></span>

2. <span data-ttu-id="5249c-272">Na **jak chcesz użytkownikom zalogować się do usługi ServiceNow** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="5249c-272">On the **How would you like users to sign on to ServiceNow** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="5249c-273">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC749324.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-273">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749324.png "Configure single sign-on")</span></span>

3. <span data-ttu-id="5249c-274">Na **Konfigurowanie ustawień aplikacji** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5249c-274">On the **Configure App Settings** page, perform the following steps:</span></span>
   
    <span data-ttu-id="5249c-275">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/IC769497.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="5249c-275">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC769497.png "Configure app URL")</span></span>
   
    <span data-ttu-id="5249c-276">a.</span><span class="sxs-lookup"><span data-stu-id="5249c-276">a.</span></span> <span data-ttu-id="5249c-277">w **usługi ServiceNow na adres URL logowania** tekstowym, wpisz adres URL używany przez użytkowników do logowania jednokrotnego do aplikacji usługi ServiceNow zgodnie ze wzorcem: `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="5249c-277">in the **ServiceNow Sign On URL** textbox, type your URL used by your users to sign-on to your ServiceNow application following the pattern: `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="5249c-278">b.</span><span class="sxs-lookup"><span data-stu-id="5249c-278">b.</span></span> <span data-ttu-id="5249c-279">W **adres URL wystawcy** tekstowym, wpisz adres URL używany przez użytkowników do logowania jednokrotnego do aplikacji usługi ServiceNow zgodnie ze wzorcem `https://<instance-name>.service-now.com`.</span><span class="sxs-lookup"><span data-stu-id="5249c-279">In the **Issuer URL** textbox,type your URL used by your users to sign-on to your ServiceNow application following the pattern `https://<instance-name>.service-now.com`.</span></span>
   
    <span data-ttu-id="5249c-280">c.</span><span class="sxs-lookup"><span data-stu-id="5249c-280">c.</span></span> <span data-ttu-id="5249c-281">Kliknij przycisk **Dalej**</span><span class="sxs-lookup"><span data-stu-id="5249c-281">Click **Next**</span></span>

4. <span data-ttu-id="5249c-282">Kliknij przycisk **ręcznie skonfigurować aplikację do logowania jednokrotnego**, następnie kliknij przycisk **dalej** i wykonaj następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="5249c-282">Click **Manually configure the application for single sign-on**, then click **Next** and complete the following steps.</span></span>
   
    <span data-ttu-id="5249c-283">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="5249c-283">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/IC7694971.png "Configure app URL")</span></span>

5. <span data-ttu-id="5249c-284">Na **skonfigurować logowanie jednokrotne w ServiceNow** kliknij przycisk **pobierania certyfikatu**, Zapisz plik certyfikatu lokalnie na komputerze, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="5249c-284">On the **Configure single sign-on at ServiceNow** page, click **Download certificate**, save the certificate file locally on your computer, and then click **Next**.</span></span>
   
    <span data-ttu-id="5249c-285">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC749325.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-285">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC749325.png "Configure single sign-on")</span></span>

6. <span data-ttu-id="5249c-286">Logowanie do aplikacji usługi ServiceNow Express jako administrator.</span><span class="sxs-lookup"><span data-stu-id="5249c-286">Sign-on to your ServiceNow Express application as an administrator.</span></span>

7. <span data-ttu-id="5249c-287">W okienku nawigacji po lewej stronie kliknij **rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="5249c-287">In the navigation pane on the left side, click **Single Sign-On**.</span></span>  
   
    <span data-ttu-id="5249c-288">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="5249c-288">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694980ex.png "Configure app URL")</span></span>

8. <span data-ttu-id="5249c-289">Na **rejestracji jednokrotnej** okna dialogowego, kliknij ikonę konfiguracji w prawym górnym rogu i ustaw następujące właściwości:</span><span class="sxs-lookup"><span data-stu-id="5249c-289">On the **Single Sign-On** dialog, click the configuration icon on the upper right and set the following properties:</span></span>
   
    <span data-ttu-id="5249c-290">![Skonfiguruj adres URL aplikacji](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "skonfigurować adres URL aplikacji")</span><span class="sxs-lookup"><span data-stu-id="5249c-290">![Configure app URL](./media/active-directory-saas-servicenow-tutorial/ic7694981ex.png "Configure app URL")</span></span>
   
    <span data-ttu-id="5249c-291">a.</span><span class="sxs-lookup"><span data-stu-id="5249c-291">a.</span></span> <span data-ttu-id="5249c-292">Przełącz **włączyć wiele dostawcy logowania jednokrotnego** z prawej strony.</span><span class="sxs-lookup"><span data-stu-id="5249c-292">Toggle **Enable multiple provider SSO** to the right.</span></span>
   
    <span data-ttu-id="5249c-293">b.</span><span class="sxs-lookup"><span data-stu-id="5249c-293">b.</span></span> <span data-ttu-id="5249c-294">Przełącz **debugowania Włącz rejestrowanie dla wielu dostawcy logowania jednokrotnego integracji** z prawej strony.</span><span class="sxs-lookup"><span data-stu-id="5249c-294">Toggle **Enable debug logging for the multiple provider SSO integration** to the right.</span></span>
   
    <span data-ttu-id="5249c-295">c.</span><span class="sxs-lookup"><span data-stu-id="5249c-295">c.</span></span> <span data-ttu-id="5249c-296">W **tabeli pole użytkownika, który...**  pole tekstowe, typ **nazwa_użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="5249c-296">In **The field on the user table that...** textbox, type **user_name**.</span></span>
9. <span data-ttu-id="5249c-297">Na **rejestracji jednokrotnej** okna dialogowego, kliknij przycisk **Dodaj nowy certyfikat**.</span><span class="sxs-lookup"><span data-stu-id="5249c-297">On the **Single Sign-On** dialog, click **Add New Certificate**.</span></span>
   
    <span data-ttu-id="5249c-298">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-298">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694973ex.png "Configure single sign-on")</span></span>
10. <span data-ttu-id="5249c-299">Na **certyfikatów X.509** okna dialogowego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5249c-299">On the **X.509 Certificates** dialog, perform the following steps:</span></span>
    
    <span data-ttu-id="5249c-300">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-300">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694975.png "Configure single sign-on")</span></span>
    
    <span data-ttu-id="5249c-301">a.</span><span class="sxs-lookup"><span data-stu-id="5249c-301">a.</span></span> <span data-ttu-id="5249c-302">W **nazwa** tekstowym, wpisz nazwę konfiguracji (np.: **TestSAML2.0**).</span><span class="sxs-lookup"><span data-stu-id="5249c-302">In the **Name** textbox, type a name for your configuration (e.g.: **TestSAML2.0**).</span></span>
    
    <span data-ttu-id="5249c-303">b.</span><span class="sxs-lookup"><span data-stu-id="5249c-303">b.</span></span> <span data-ttu-id="5249c-304">Wybierz **Active**.</span><span class="sxs-lookup"><span data-stu-id="5249c-304">Select **Active**.</span></span>
    
    <span data-ttu-id="5249c-305">c.</span><span class="sxs-lookup"><span data-stu-id="5249c-305">c.</span></span> <span data-ttu-id="5249c-306">Jako **Format**, wybierz pozycję **PEM**.</span><span class="sxs-lookup"><span data-stu-id="5249c-306">As **Format**, select **PEM**.</span></span>
    
    <span data-ttu-id="5249c-307">d.</span><span class="sxs-lookup"><span data-stu-id="5249c-307">d.</span></span> <span data-ttu-id="5249c-308">Jako **typu**, wybierz pozycję **zaufania certyfikatów magazynu**.</span><span class="sxs-lookup"><span data-stu-id="5249c-308">As **Type**, select **Trust Store Cert**.</span></span>
    
    <span data-ttu-id="5249c-309">e.</span><span class="sxs-lookup"><span data-stu-id="5249c-309">e.</span></span> <span data-ttu-id="5249c-310">Utwórz plik kodowany w standardzie Base64 z pobranego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="5249c-310">Create a Base64 encoded file from your downloaded certificate.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="5249c-311">Aby uzyskać więcej informacji, zobacz [sposób konwertowania binarne certyfikatu do pliku tekstowego](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="5249c-311">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>
    > 
    > 
    
    <span data-ttu-id="5249c-312">f.</span><span class="sxs-lookup"><span data-stu-id="5249c-312">f.</span></span> <span data-ttu-id="5249c-313">Otwórz w Notatniku Twojego certyfikatu szyfrowania Base64, skopiuj zawartość go do Schowka, a następnie wklej go do **certyfikatu PEM** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5249c-313">Open your Base64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **PEM Certificate** textbox.</span></span>
    
    <span data-ttu-id="5249c-314">g.</span><span class="sxs-lookup"><span data-stu-id="5249c-314">g.</span></span> <span data-ttu-id="5249c-315">Kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="5249c-315">Click **Update**.</span></span>
11. <span data-ttu-id="5249c-316">Na **rejestracji jednokrotnej** okna dialogowego, kliknij przycisk **Dodaj nowe IdP**.</span><span class="sxs-lookup"><span data-stu-id="5249c-316">On the **Single Sign-On** dialog, click **Add New IdP**.</span></span>
    
    <span data-ttu-id="5249c-317">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-317">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694976ex.png "Configure single sign-on")</span></span>
12. <span data-ttu-id="5249c-318">Na **Dodaj nowego dostawcę tożsamości** okna dialogowego, w obszarze **Konfigurowanie dostawcy tożsamości**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5249c-318">On the **Add New Identity Provider** dialog, under **Configure Identity Provider**, perform the following steps:</span></span>
    
    <span data-ttu-id="5249c-319">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-319">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694982ex.png "Configure single sign-on")</span></span>

    <span data-ttu-id="5249c-320">a.</span><span class="sxs-lookup"><span data-stu-id="5249c-320">a.</span></span> <span data-ttu-id="5249c-321">w **nazwa** tekstowym, wpisz nazwę konfiguracji (np.: **SAML 2.0**).</span><span class="sxs-lookup"><span data-stu-id="5249c-321">In the **Name** textbox, type a name for your configuration (e.g.: **SAML 2.0**).</span></span>

    <span data-ttu-id="5249c-322">b.</span><span class="sxs-lookup"><span data-stu-id="5249c-322">b.</span></span> <span data-ttu-id="5249c-323">W klasycznym portalu usługi Azure AD, skopiuj **identyfikator dostawcy tożsamości** wartość, a następnie wklej ją do **adres URL dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5249c-323">In the Azure AD classic portal, copy the **Identity Provider ID** value, and then paste it into the **Identity Provider URL** textbox.</span></span>

    <span data-ttu-id="5249c-324">c.</span><span class="sxs-lookup"><span data-stu-id="5249c-324">c.</span></span> <span data-ttu-id="5249c-325">W klasycznym portalu usługi Azure AD, skopiuj **adres URL żądania uwierzytelniania** wartość, a następnie wklej ją do **AuthnRequest dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5249c-325">In the Azure AD classic portal, copy the **Authentication Request URL** value, and then paste it into the **Identity Provider's AuthnRequest** textbox.</span></span>

    <span data-ttu-id="5249c-326">d.</span><span class="sxs-lookup"><span data-stu-id="5249c-326">d.</span></span> <span data-ttu-id="5249c-327">W klasycznym portalu usługi Azure AD, skopiuj **pojedynczy adres URL usługi Sign-Out** wartość, a następnie wklej ją do **SingleLogoutRequest dostawcy tożsamości** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="5249c-327">In the Azure AD classic portal, copy the **Single Sign-Out Service URL** value, and then paste it into the **Identity Provider's SingleLogoutRequest** textbox.</span></span>

    <span data-ttu-id="5249c-328">e.</span><span class="sxs-lookup"><span data-stu-id="5249c-328">e.</span></span> <span data-ttu-id="5249c-329">Jako **certyfikat dostawcy tożsamości**, wybierz certyfikat został utworzony w poprzednim kroku.</span><span class="sxs-lookup"><span data-stu-id="5249c-329">As **Identity Provider Certificate**, select the certificate you have created in the previous step.</span></span>


1. <span data-ttu-id="5249c-330">Kliknij przycisk **Zaawansowane ustawienia**, a następnie w obszarze **dodatkowe właściwości dostawcy tożsamości**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5249c-330">Click **Advanced Settings**, and under **Additional Identity Provider Properties**, perform the following steps:</span></span>
   
    <span data-ttu-id="5249c-331">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-331">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694983ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="5249c-332">a.</span><span class="sxs-lookup"><span data-stu-id="5249c-332">a.</span></span> <span data-ttu-id="5249c-333">W **powiązanie protokołu IDP SingleLogoutRequest** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:2.0:bindings:HTTP-przekierowania**.</span><span class="sxs-lookup"><span data-stu-id="5249c-333">In the **Protocol Binding for the IDP's SingleLogoutRequest** textbox, type **urn:oasis:names:tc:SAML:2.0:bindings:HTTP-Redirect**.</span></span>
   
    <span data-ttu-id="5249c-334">b.</span><span class="sxs-lookup"><span data-stu-id="5249c-334">b.</span></span> <span data-ttu-id="5249c-335">W **zasad NameID** pole tekstowe, typ **urn: oasis: nazwy: tc: SAML:1.1:nameid-format: nieokreślony**.</span><span class="sxs-lookup"><span data-stu-id="5249c-335">In the **NameID Policy** textbox, type **urn:oasis:names:tc:SAML:1.1:nameid-format:unspecified**.</span></span>    
   
    <span data-ttu-id="5249c-336">c.</span><span class="sxs-lookup"><span data-stu-id="5249c-336">c.</span></span> <span data-ttu-id="5249c-337">W **metody AuthnContextClassRef**, typ **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span><span class="sxs-lookup"><span data-stu-id="5249c-337">In the **AuthnContextClassRef Method**, type **http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password**.</span></span>
   
    <span data-ttu-id="5249c-338">d.</span><span class="sxs-lookup"><span data-stu-id="5249c-338">d.</span></span> <span data-ttu-id="5249c-339">Anuluj wybór **utworzyć AuthnContextClass**.</span><span class="sxs-lookup"><span data-stu-id="5249c-339">Deselect **Create an AuthnContextClass**.</span></span>

2. <span data-ttu-id="5249c-340">W obszarze **dodatkowe właściwości dostawcy usług**, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5249c-340">Under **Additional Service Provider Properties**, perform the following steps:</span></span>
   
    <span data-ttu-id="5249c-341">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-341">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/ic7694984ex.png "Configure single sign-on")</span></span>
   
    <span data-ttu-id="5249c-342">a.</span><span class="sxs-lookup"><span data-stu-id="5249c-342">a.</span></span> <span data-ttu-id="5249c-343">W **strony głównej usługi ServiceNow** tekstowym, wpisz adres URL strony głównej wystąpienia usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="5249c-343">In the **ServiceNow Homepage** textbox, type the URL of your ServiceNow instance homepage.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="5249c-344">Na stronie głównej wystąpienia usługi ServiceNow jest złączeniem Twojej **adres URL dzierżawy ServieNow** i **/navpage.do** (np.: `https://fabrikam.service-now.com/navpage.do`).</span><span class="sxs-lookup"><span data-stu-id="5249c-344">The ServiceNow instance homepage is a concatenation of your **ServieNow tenant URL** and **/navpage.do** (e.g.: `https://fabrikam.service-now.com/navpage.do`).</span></span>
    > 
    > 
   
    <span data-ttu-id="5249c-345">b.</span><span class="sxs-lookup"><span data-stu-id="5249c-345">b.</span></span> <span data-ttu-id="5249c-346">W **identyfikator podmiot / wystawca** pole tekstowe, wpisz adres URL dzierżawy usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="5249c-346">In the **Entity ID / Issuer** textbox, type the URL of your ServiceNow tenant.</span></span>
   
    <span data-ttu-id="5249c-347">c.</span><span class="sxs-lookup"><span data-stu-id="5249c-347">c.</span></span> <span data-ttu-id="5249c-348">W **identyfikatora URI odbiorców** tekstowym, wpisz adres URL dzierżawy usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="5249c-348">In the **Audience URI** textbox, type the URL of your ServiceNow tenant.</span></span> 
   
    <span data-ttu-id="5249c-349">d.</span><span class="sxs-lookup"><span data-stu-id="5249c-349">d.</span></span> <span data-ttu-id="5249c-350">W **pochylanie zegara** pole tekstowe, typ **60**.</span><span class="sxs-lookup"><span data-stu-id="5249c-350">In **Clock Skew** textbox, type **60**.</span></span>
   
    <span data-ttu-id="5249c-351">e.</span><span class="sxs-lookup"><span data-stu-id="5249c-351">e.</span></span> <span data-ttu-id="5249c-352">W **pole użytkownika** pole tekstowe, typ **e-mail** lub **nazwa_użytkownika**, w zależności od pole, które jest używane do unikatowego identyfikowania użytkowników w danym wdrożeniu usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="5249c-352">In the **User Field** textbox, type **email** or **user_name**, depending on which field is used to uniquely identify users in your ServiceNow deployment.</span></span>
   
    > [!NOTE]
    > <span data-ttu-id="5249c-353">Można configue usługi Azure AD, aby emitować identyfikator użytkownika usługi Azure AD (główna nazwa użytkownika) lub adres e-mail jako unikatowy identyfikator w tokenie SAML, przechodząc do **ServiceNow > atrybuty > logowanie jednokrotne** sekcji klasyczny Portal Azure Portal i mapowanie odpowiednie pola **nameidentifier** atrybutu.</span><span class="sxs-lookup"><span data-stu-id="5249c-353">You can configue Azure AD to emit either the Azure AD user ID (user principal name) or the email address as the unique identifier in the SAML token by going to the **ServiceNow > Attributes > Single Sign-On** section of the Azure classic portal and mapping the desired field to the **nameidentifier** attribute.</span></span> <span data-ttu-id="5249c-354">Wartość przechowywana wybranego atrybutu w usłudze Azure AD (np. główna nazwa użytkownika) musi odpowiadać wartości przechowywane w usługi ServiceNow wprowadzony w polu (np. nazwa_użytkownika)</span><span class="sxs-lookup"><span data-stu-id="5249c-354">The value stored for the selected attribute in Azure AD (e.g. user principal name) must match the value stored in ServiceNow for the entered field (e.g. user_name)</span></span>
    > 
    > 
   
    <span data-ttu-id="5249c-355">f.</span><span class="sxs-lookup"><span data-stu-id="5249c-355">f.</span></span> <span data-ttu-id="5249c-356">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="5249c-356">Click **Save**.</span></span> 

3. <span data-ttu-id="5249c-357">W klasycznym portalu usługi Azure AD, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij **dalej**.</span><span class="sxs-lookup"><span data-stu-id="5249c-357">On the Azure AD classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    <span data-ttu-id="5249c-358">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-358">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694990.png "Configure single sign-on")</span></span>

4. <span data-ttu-id="5249c-359">Na **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="5249c-359">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    <span data-ttu-id="5249c-360">![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "skonfigurować logowanie jednokrotne")</span><span class="sxs-lookup"><span data-stu-id="5249c-360">![Configure single sign-on](./media/active-directory-saas-servicenow-tutorial/IC7694991.png "Configure single sign-on")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="5249c-361">Konfigurowanie Inicjowanie obsługi użytkowników</span><span class="sxs-lookup"><span data-stu-id="5249c-361">Configuring user provisioning</span></span>
<span data-ttu-id="5249c-362">Celem tej sekcji jest przedstawiają sposób włączania kont użytkowników usługi Active Directory do usługi ServiceNow Inicjowanie obsługi użytkowników.</span><span class="sxs-lookup"><span data-stu-id="5249c-362">The objective of this section is to outline how to enable user provisioning of Active Directory user accounts to ServiceNow.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="5249c-363">Aby skonfigurować, inicjowanie obsługi użytkowników, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5249c-363">To configure user provisioning, perform the following steps:</span></span>
1. <span data-ttu-id="5249c-364">W klasycznym portalu Azure Management na **ServiceNow** strona integracji aplikacji, kliknij przycisk **skonfigurować Inicjowanie obsługi użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="5249c-364">In the Azure Management classic portal, on the **ServiceNow** application integration page, click **Configure user provisioning**.</span></span> 
   
    <span data-ttu-id="5249c-365">![Inicjowanie obsługi użytkowników](./media/active-directory-saas-servicenow-tutorial/IC769498.png "Inicjowanie obsługi użytkowników")</span><span class="sxs-lookup"><span data-stu-id="5249c-365">![User provisioning](./media/active-directory-saas-servicenow-tutorial/IC769498.png "User provisioning")</span></span>

2. <span data-ttu-id="5249c-366">Na **wprowadź swoje poświadczenia usługi ServiceNow, aby umożliwić inicjowanie obsługi użytkowników automatyczne** Podaj następujące ustawienia konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="5249c-366">On the **Enter your ServiceNow credentials to enable automatic user provisioning** page, provide the following configuration settings:</span></span>
   
     <span data-ttu-id="5249c-367">a.</span><span class="sxs-lookup"><span data-stu-id="5249c-367">a.</span></span> <span data-ttu-id="5249c-368">W **nazwy wystąpienia usługi ServiceNow** tekstowym, wpisz nazwę wystąpienia usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="5249c-368">In the **ServiceNow Instance Name** textbox, type the ServiceNow instance name.</span></span>
   
     <span data-ttu-id="5249c-369">b.</span><span class="sxs-lookup"><span data-stu-id="5249c-369">b.</span></span> <span data-ttu-id="5249c-370">W **nazwa użytkownika administratora usługi ServiceNow** tekstowym, wpisz nazwę konta administratora usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="5249c-370">In the **ServiceNow Admin User Name** textbox, type the name of the ServiceNow admin account.</span></span>
   
     <span data-ttu-id="5249c-371">c.</span><span class="sxs-lookup"><span data-stu-id="5249c-371">c.</span></span> <span data-ttu-id="5249c-372">W **hasło administratora usługi ServiceNow** tekstowym, wpisz hasło dla tego konta.</span><span class="sxs-lookup"><span data-stu-id="5249c-372">In the **ServiceNow Admin Password** textbox, type the password for this account.</span></span>
   
     <span data-ttu-id="5249c-373">d.</span><span class="sxs-lookup"><span data-stu-id="5249c-373">d.</span></span> <span data-ttu-id="5249c-374">Kliknij przycisk **zweryfikować** Aby zweryfikować konfigurację.</span><span class="sxs-lookup"><span data-stu-id="5249c-374">Click **validate** to verify your configuration.</span></span>
   
     <span data-ttu-id="5249c-375">e.</span><span class="sxs-lookup"><span data-stu-id="5249c-375">e.</span></span> <span data-ttu-id="5249c-376">Kliknij przycisk **dalej** przycisk, aby otworzyć **następne kroki** strony.</span><span class="sxs-lookup"><span data-stu-id="5249c-376">Click the **Next** button to open the **Next steps** page.</span></span>
   
     <span data-ttu-id="5249c-377">f.</span><span class="sxs-lookup"><span data-stu-id="5249c-377">f.</span></span> <span data-ttu-id="5249c-378">Jeśli chcesz udostępnić wszystkim użytkownikom na tę aplikację, wybierz opcję "**automatycznie obsługiwać wszystkie konta użytkowników w katalogu do tej aplikacji**".</span><span class="sxs-lookup"><span data-stu-id="5249c-378">If you want to provision all users to this application, select “**Automatically provision all user accounts in the directory to this application**”.</span></span> 
   
    <span data-ttu-id="5249c-379">![Następne kroki](./media/active-directory-saas-servicenow-tutorial/IC698804.png "następne kroki")</span><span class="sxs-lookup"><span data-stu-id="5249c-379">![Next Steps](./media/active-directory-saas-servicenow-tutorial/IC698804.png "Next Steps")</span></span>
   
     <span data-ttu-id="5249c-380">g.</span><span class="sxs-lookup"><span data-stu-id="5249c-380">g.</span></span> <span data-ttu-id="5249c-381">Na **następne kroki** kliknij przycisk **Complete** Aby zapisać konfigurację.</span><span class="sxs-lookup"><span data-stu-id="5249c-381">On the **Next steps** page, click **Complete** to save your configuration.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5249c-382">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5249c-382">Creating an Azure AD test user</span></span>
<span data-ttu-id="5249c-383">W tej sekcji utworzysz użytkownika testowego w klasycznym portalu o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="5249c-383">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][20]

<span data-ttu-id="5249c-385">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5249c-385">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5249c-386">W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5249c-386">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="5249c-388">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="5249c-388">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="5249c-389">Aby wyświetlić listę użytkowników, w menu u góry, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="5249c-389">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5249c-391">Aby otworzyć **Dodaj użytkownika** okna dialogowego na pasku narzędzi u dołu, kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="5249c-391">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="5249c-393">Na **Poinformuj nas o tym użytkowniku** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5249c-393">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="5249c-395">a.</span><span class="sxs-lookup"><span data-stu-id="5249c-395">a.</span></span> <span data-ttu-id="5249c-396">Jako typ użytkownika wybierz nowego użytkownika w organizacji.</span><span class="sxs-lookup"><span data-stu-id="5249c-396">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="5249c-397">b.</span><span class="sxs-lookup"><span data-stu-id="5249c-397">b.</span></span> <span data-ttu-id="5249c-398">W nazwie użytkownika **pole tekstowe**, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5249c-398">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="5249c-399">c.</span><span class="sxs-lookup"><span data-stu-id="5249c-399">c.</span></span> <span data-ttu-id="5249c-400">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="5249c-400">Click **Next**.</span></span>

6. <span data-ttu-id="5249c-401">Na **profilu użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5249c-401">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_06.png) 
   
   <span data-ttu-id="5249c-403">a.</span><span class="sxs-lookup"><span data-stu-id="5249c-403">a.</span></span> <span data-ttu-id="5249c-404">W **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="5249c-404">In the **First Name** textbox, type **Britta**.</span></span>  
   
   <span data-ttu-id="5249c-405">b.</span><span class="sxs-lookup"><span data-stu-id="5249c-405">b.</span></span> <span data-ttu-id="5249c-406">W **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="5249c-406">In the **Last Name** textbox, type, **Simon**.</span></span>
   
   <span data-ttu-id="5249c-407">c.</span><span class="sxs-lookup"><span data-stu-id="5249c-407">c.</span></span> <span data-ttu-id="5249c-408">W **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="5249c-408">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
   <span data-ttu-id="5249c-409">d.</span><span class="sxs-lookup"><span data-stu-id="5249c-409">d.</span></span> <span data-ttu-id="5249c-410">W **roli** listy, wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="5249c-410">In the **Role** list, select **User**.</span></span>
   
   <span data-ttu-id="5249c-411">e.</span><span class="sxs-lookup"><span data-stu-id="5249c-411">e.</span></span> <span data-ttu-id="5249c-412">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="5249c-412">Click **Next**.</span></span>

7. <span data-ttu-id="5249c-413">Na **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="5249c-413">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="5249c-415">Na **Uzyskaj hasło tymczasowe** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="5249c-415">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-servicenow-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="5249c-417">a.</span><span class="sxs-lookup"><span data-stu-id="5249c-417">a.</span></span> <span data-ttu-id="5249c-418">Zanotuj wartość **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="5249c-418">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="5249c-419">b.</span><span class="sxs-lookup"><span data-stu-id="5249c-419">b.</span></span> <span data-ttu-id="5249c-420">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="5249c-420">Click **Complete**.</span></span>   

### <a name="creating-a-servicenow-test-user"></a><span data-ttu-id="5249c-421">Tworzenie użytkownika testowego usługi ServiceNow</span><span class="sxs-lookup"><span data-stu-id="5249c-421">Creating a ServiceNow test user</span></span>
<span data-ttu-id="5249c-422">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="5249c-422">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="5249c-423">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="5249c-423">In this section, you create a user called Britta Simon in ServiceNow.</span></span> <span data-ttu-id="5249c-424">Jeśli nie wiadomo, jak dodać użytkownika w ramach konta usługi ServiceNow lub usługi ServiceNow Express, skontaktuj się z zespołem pomocy technicznej usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="5249c-424">If you don't know how to add a user in your ServiceNow or ServiceNow Express account, contact ServiceNow support team.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5249c-425">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="5249c-425">Assigning the Azure AD test user</span></span>
<span data-ttu-id="5249c-426">W tej sekcji można włączyć Simona Britta na udostępnienie jej do usługi ServiceNow za pomocą usługi Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="5249c-426">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to ServiceNow.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="5249c-428">**Aby przypisać Simona Britta usługi ServiceNow, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="5249c-428">**To assign Britta Simon to ServiceNow, perform the following steps:**</span></span>

1. <span data-ttu-id="5249c-429">W klasycznym portalu, aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="5249c-429">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="5249c-431">Na liście aplikacji zaznacz **ServiceNow**.</span><span class="sxs-lookup"><span data-stu-id="5249c-431">In the applications list, select **ServiceNow**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-servicenow-tutorial/tutorial_servicenow_10.png) 

3. <span data-ttu-id="5249c-433">W menu u góry kliknij **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="5249c-433">In the menu on the top, click **Users**.</span></span>
   
    ![Przypisz użytkownika][203] 

4. <span data-ttu-id="5249c-435">Na liście wszystkich użytkowników, wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="5249c-435">In the All Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="5249c-436">Na pasku narzędzi u dołu, kliknij przycisk **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="5249c-436">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Przypisz użytkownika][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="5249c-438">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="5249c-438">Testing single sign-on</span></span>
<span data-ttu-id="5249c-439">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="5249c-439">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5249c-440">Po kliknięciu kafelka usługi ServiceNow w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji usługi ServiceNow.</span><span class="sxs-lookup"><span data-stu-id="5249c-440">When you click the ServiceNow tile in the Access Panel, you should get automatically signed-on to your ServiceNow application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5249c-441">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="5249c-441">Additional resources</span></span>
* [<span data-ttu-id="5249c-442">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5249c-442">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5249c-443">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5249c-443">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_04.png


[5]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_05.png
[6]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_06.png
[7]:  ./media/active-directory-saas-servicenow-tutorial/tutorial_general_050.png
[10]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_060.png
[11]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_070.png
[20]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-servicenow-tutorial/tutorial_general_205.png
