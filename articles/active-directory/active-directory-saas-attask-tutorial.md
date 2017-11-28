---
title: 'Samouczek: Integracji Azure Active Directory z @Task| Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i @Task."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: aab8bd2f-f9dd-42da-a18e-d707865687d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: ebb19ca6cbaf04106fbce937d95651e709854cfd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-task"></a><span data-ttu-id="7c4df-103">Samouczek: Integracji Azure Active Directory z@Task</span><span class="sxs-lookup"><span data-stu-id="7c4df-103">Tutorial: Azure Active Directory integration with @Task</span></span>
<span data-ttu-id="7c4df-104">Celem tego samouczka jest pokazano, jak zintegrować @Task z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7c4df-104">The objective of this tutorial is to show you how to integrate @Task with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="7c4df-105">Integrowanie @Task z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="7c4df-105">Integrating @Task with Azure AD provides you with the following benefits:</span></span> 

* <span data-ttu-id="7c4df-106">Można kontrolować w usłudze Azure AD, kto ma dostęp@Task</span><span class="sxs-lookup"><span data-stu-id="7c4df-106">You can control in Azure AD who has access to @Task</span></span>
* <span data-ttu-id="7c4df-107">Można umożliwić użytkownikom automatycznie pobrać zalogowane do @Task (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c4df-107">You can enable your users to automatically get signed-on to @Task (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="7c4df-108">Możesz zarządzać kont w jednej centralnej lokalizacji - klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="7c4df-108">You can manage your accounts in one central location - the Azure classic Portal</span></span>

<span data-ttu-id="7c4df-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7c4df-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c4df-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="7c4df-110">Prerequisites</span></span>
<span data-ttu-id="7c4df-111">Aby skonfigurować integrację usługi Azure AD z @Task, potrzebne są następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="7c4df-111">To configure Azure AD integration with @Task, you need the following items:</span></span>

* <span data-ttu-id="7c4df-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c4df-112">An Azure AD subscription</span></span>
* <span data-ttu-id="7c4df-113">@Task Jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="7c4df-113">An @Task single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7c4df-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="7c4df-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="7c4df-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="7c4df-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="7c4df-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="7c4df-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="7c4df-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7c4df-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span> 

## <a name="scenario-description"></a><span data-ttu-id="7c4df-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="7c4df-118">Scenario Description</span></span>
<span data-ttu-id="7c4df-119">Celem tego samouczka jest umożliwienie umożliwia testowanie usługi Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="7c4df-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="7c4df-120">Scenariusz opisany w tym samouczku składa się z trzech głównych bloków konstrukcyjnych:</span><span class="sxs-lookup"><span data-stu-id="7c4df-120">The scenario outlined in this tutorial consists of three main building blocks:</span></span>

1. <span data-ttu-id="7c4df-121">Dodawanie @Task z galerii</span><span class="sxs-lookup"><span data-stu-id="7c4df-121">Adding @Task from the gallery</span></span> 
2. <span data-ttu-id="7c4df-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7c4df-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-task-from-the-gallery"></a><span data-ttu-id="7c4df-123">Dodawanie @Task z galerii</span><span class="sxs-lookup"><span data-stu-id="7c4df-123">Adding @Task from the gallery</span></span>
<span data-ttu-id="7c4df-124">Aby skonfigurować integrację @Task do usługi Azure AD, należy dodać @Task z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="7c4df-124">To configure the integration of @Task into Azure AD, you need to add @Task from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7c4df-125">**Aby dodać @Task z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7c4df-125">**To add @Task from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7c4df-126">W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Usługa Active Directory][1] 
2. <span data-ttu-id="7c4df-128">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="7c4df-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="7c4df-129">Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="7c4df-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Aplikacje][2] 
4. <span data-ttu-id="7c4df-131">Kliknij przycisk **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="7c4df-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplikacje][3] 
5. <span data-ttu-id="7c4df-133">Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Aplikacje][4] 
6. <span data-ttu-id="7c4df-135">W polu wyszukiwania wpisz  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="7c4df-135">In the search box, type **@Task**.</span></span>
   
    ![Aplikacje][5] 
7. <span data-ttu-id="7c4df-137">W okienku wyników wybierz  **@Task** , a następnie kliknij przycisk **Complete** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="7c4df-137">In the results pane, select **@Task**, and then click **Complete** to add the application.</span></span>
   
    ![Aplikacje][30] 

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7c4df-139">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="7c4df-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7c4df-140">Celem tej sekcji jest opisano, jak skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z @Task w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="7c4df-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with @Task based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="7c4df-141">Dla rejestracji jednokrotnej do pracy, usługi Azure AD musi wiedzieć, jaki użytkownik odpowiednika w @Task użytkownika w usłudze Azure AD jest.</span><span class="sxs-lookup"><span data-stu-id="7c4df-141">For single sign-on to work, Azure AD needs to know what the counterpart user in @Task to an user in Azure AD is.</span></span> <span data-ttu-id="7c4df-142">Innymi słowy, relacja linku między użytkownika usługi Azure AD i danemu użytkownikowi w @Task należy ustanowić.</span><span class="sxs-lookup"><span data-stu-id="7c4df-142">In other words, a link relationship between an Azure AD user and the related user in @Task needs to be established.</span></span>   
<span data-ttu-id="7c4df-143">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w @Task.</span><span class="sxs-lookup"><span data-stu-id="7c4df-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in @Task.</span></span>

<span data-ttu-id="7c4df-144">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z @Task, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="7c4df-144">To configure and test Azure AD single sign-on with @Task, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7c4df-145">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="7c4df-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7c4df-146">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7c4df-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7c4df-147">**[Tworzenie @Tasktest użytkownika](#creating-a-halogen-software-test-user)**  — aby odpowiednikiem Simona Britta w @Taskthat jest połączona z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7c4df-147">**[Creating a @Tasktest user](#creating-a-halogen-software-test-user)** - to have a counterpart of Britta Simon in @Taskthat is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="7c4df-148">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="7c4df-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7c4df-149">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="7c4df-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7c4df-150">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7c4df-150">Configuring Azure AD Single Sign-On</span></span>
<span data-ttu-id="7c4df-151">Celem tej sekcji jest do włączenia usługi Azure AD rejestracji jednokrotnej w klasycznym portalu Azure i konfigurowania rejestracji jednokrotnej w sieci @Task aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7c4df-151">The objective of this section is to enable Azure AD single sign-on in the Azure classic portal and to configure single sign-on in your @Task application.</span></span>

<span data-ttu-id="7c4df-152">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z @Task, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7c4df-152">**To configure Azure AD single sign-on with @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="7c4df-153">W klasycznym portalu Azure na  **@Task**  strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować logowanie jednokrotne** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="7c4df-153">In the Azure classic portal, on the **@Task** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][6] 
2. <span data-ttu-id="7c4df-155">Na **jak chcesz użytkownikom logowanie się @Task**  wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-155">On the **How would you like users to sign on to @Task** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][7] 
3. <span data-ttu-id="7c4df-157">Na **Konfigurowanie ustawień aplikacji** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7c4df-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>
   
    ![Konfiguruj ustawienia aplikacji][8] 
   
     <span data-ttu-id="7c4df-159">a.</span><span class="sxs-lookup"><span data-stu-id="7c4df-159">a.</span></span> <span data-ttu-id="7c4df-160">W **na adres URL logowania** tekstowym, wpisz adres URL używany przez użytkowników do logowania jednokrotnego w sieci @Task aplikacji (np.:*https://<Tenant name>.attask ondemand.com*).</span><span class="sxs-lookup"><span data-stu-id="7c4df-160">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your @Task application (e.g.:*https://<Tenant name>.attask-ondemand.com*).</span></span>
   
     <span data-ttu-id="7c4df-161">b.</span><span class="sxs-lookup"><span data-stu-id="7c4df-161">b.</span></span> <span data-ttu-id="7c4df-162">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-162">Click **Next**.</span></span>
4. <span data-ttu-id="7c4df-163">Na **skonfigurować logowanie jednokrotne w @Task**  kliknij przycisk **pobierania metadanych**, Zapisz plik metadanych lokalnie na komputerze, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-163">On the **Configure single sign-on at @Task** page, click **Download metadata**, save the metadata file locally on your computer, and then click **Next**.</span></span>
   
    ![Co to jest program Azure AD Connect][9] 
5. <span data-ttu-id="7c4df-165">Logowanie do Twojej @Task witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="7c4df-165">Sign-on to your @Task company site as administrator.</span></span>
6. <span data-ttu-id="7c4df-166">Przejdź do **Rejestracja jednokrotna w konfiguracji**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-166">Go to **Single Sign On Configuration**.</span></span>
7. <span data-ttu-id="7c4df-167">Na **rejestracji jednokrotnej** okna dialogowego, wykonaj następujące czynności</span><span class="sxs-lookup"><span data-stu-id="7c4df-167">On the **Single Sign-On** dialog, perform the following steps</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][23]
   
    <span data-ttu-id="7c4df-169">a.</span><span class="sxs-lookup"><span data-stu-id="7c4df-169">a.</span></span> <span data-ttu-id="7c4df-170">Jako **typu**, wybierz pozycję **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-170">As **Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="7c4df-171">b.</span><span class="sxs-lookup"><span data-stu-id="7c4df-171">b.</span></span> <span data-ttu-id="7c4df-172">Wybierz **usługi identyfikator dostawcy**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-172">Select **Service Provider ID**.</span></span>
   
    <span data-ttu-id="7c4df-173">c.</span><span class="sxs-lookup"><span data-stu-id="7c4df-173">c.</span></span> <span data-ttu-id="7c4df-174">W klasycznym portalu Azure, skopiuj **zdalnego adresu URL logowania**, a następnie wklej go do **adresu URL logowania do portalu** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="7c4df-174">On the Azure classic portal, copy the **Remote Login URL**, and then paste it into the **Login Portal URL** textbox.</span></span>
   
    <span data-ttu-id="7c4df-175">d.</span><span class="sxs-lookup"><span data-stu-id="7c4df-175">d.</span></span> <span data-ttu-id="7c4df-176">W klasycznym portalu Azure, skopiuj **pojedynczy adres URL usługi Sign-Out**, a następnie wklej go do **Sign-Out adres URL** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="7c4df-176">On the Azure classic portal, copy the **Single Sign-Out Service URL**, and then paste it into the **Sign-Out URL** textbox.</span></span>
   
    <span data-ttu-id="7c4df-177">e.</span><span class="sxs-lookup"><span data-stu-id="7c4df-177">e.</span></span> <span data-ttu-id="7c4df-178">W klasycznym portalu Azure, skopiuj **Zmień adres URL hasła**, a następnie wklej go do **Zmień adres URL hasła** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="7c4df-178">On the Azure classic portal, copy the **Change Password URL**, and then paste it into the **Change Password URL** textbox.</span></span>
   
    <span data-ttu-id="7c4df-179">f.</span><span class="sxs-lookup"><span data-stu-id="7c4df-179">f.</span></span> <span data-ttu-id="7c4df-180">Kliknij pozycję **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-180">Click **Save**.</span></span>
8. <span data-ttu-id="7c4df-181">W klasycznym portalu Azure, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-181">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span> 
   
    ![Co to jest program Azure AD Connect][10]
9. <span data-ttu-id="7c4df-183">Na **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-183">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Co to jest program Azure AD Connect][11]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7c4df-185">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c4df-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="7c4df-186">Celem tej sekcji jest tworzenie użytkownika testowego w klasycznym portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="7c4df-186">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Tworzenie użytkowników usługi Azure AD][20]

<span data-ttu-id="7c4df-188">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7c4df-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7c4df-189">W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-189">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_02.png) 
2. <span data-ttu-id="7c4df-191">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="7c4df-191">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="7c4df-192">Aby wyświetlić listę użytkowników, w menu u góry, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-192">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_03.png) 
4. <span data-ttu-id="7c4df-194">Aby otworzyć **Dodaj użytkownika** okna dialogowego na pasku narzędzi u dołu, kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-194">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_04.png) 
5. <span data-ttu-id="7c4df-196">Na **Poinformuj nas o tym użytkowniku** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7c4df-196">On the **Tell us about this user** dialog page, perform the following steps:</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_05.png) 
   
    <span data-ttu-id="7c4df-198">a.</span><span class="sxs-lookup"><span data-stu-id="7c4df-198">a.</span></span> <span data-ttu-id="7c4df-199">Jako typ użytkownika wybierz nowego użytkownika w organizacji.</span><span class="sxs-lookup"><span data-stu-id="7c4df-199">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="7c4df-200">b.</span><span class="sxs-lookup"><span data-stu-id="7c4df-200">b.</span></span> <span data-ttu-id="7c4df-201">W nazwie użytkownika **pole tekstowe**, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-201">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="7c4df-202">c.</span><span class="sxs-lookup"><span data-stu-id="7c4df-202">c.</span></span> <span data-ttu-id="7c4df-203">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-203">Click **Next**.</span></span>
6. <span data-ttu-id="7c4df-204">Na **profilu użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7c4df-204">On the **User Profile** dialog page, perform the following steps:</span></span> 
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_06.png) 
   
    <span data-ttu-id="7c4df-206">a.</span><span class="sxs-lookup"><span data-stu-id="7c4df-206">a.</span></span> <span data-ttu-id="7c4df-207">W **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-207">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="7c4df-208">b.</span><span class="sxs-lookup"><span data-stu-id="7c4df-208">b.</span></span> <span data-ttu-id="7c4df-209">W **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-209">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="7c4df-210">c.</span><span class="sxs-lookup"><span data-stu-id="7c4df-210">c.</span></span> <span data-ttu-id="7c4df-211">W **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-211">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="7c4df-212">d.</span><span class="sxs-lookup"><span data-stu-id="7c4df-212">d.</span></span> <span data-ttu-id="7c4df-213">W **roli** listy, wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-213">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="7c4df-214">e.</span><span class="sxs-lookup"><span data-stu-id="7c4df-214">e.</span></span> <span data-ttu-id="7c4df-215">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-215">Click **Next**.</span></span>

7. <span data-ttu-id="7c4df-216">Na **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-216">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_07.png) 
8. <span data-ttu-id="7c4df-218">Na **Uzyskaj hasło tymczasowe** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7c4df-218">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-attask-tutorial/create_aaduser_08.png) 
   
    <span data-ttu-id="7c4df-220">a.</span><span class="sxs-lookup"><span data-stu-id="7c4df-220">a.</span></span> <span data-ttu-id="7c4df-221">Zanotuj wartość **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-221">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="7c4df-222">b.</span><span class="sxs-lookup"><span data-stu-id="7c4df-222">b.</span></span> <span data-ttu-id="7c4df-223">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="7c4df-223">Click **Complete**.</span></span>   

### <a name="creating-an-task-test-user"></a><span data-ttu-id="7c4df-224">Tworzenie @Task użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="7c4df-224">Creating an @Task test user</span></span>
<span data-ttu-id="7c4df-225">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w @Task.</span><span class="sxs-lookup"><span data-stu-id="7c4df-225">The objective of this section is to create a user called Britta Simon in @Task.</span></span>

<span data-ttu-id="7c4df-226">**Aby utworzyć użytkownika o nazwie Simona Britta w @Task, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7c4df-226">**To create a user called Britta Simon in @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="7c4df-227">Zaloguj się na Twojej @Task witryny firmy jako administrator.</span><span class="sxs-lookup"><span data-stu-id="7c4df-227">Sign on to your @Task company site as administrator.</span></span>
2. <span data-ttu-id="7c4df-228">W menu u góry kliknij **osób**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-228">In the menu on the top, click **People**.</span></span>
3. <span data-ttu-id="7c4df-229">Kliknij przycisk **nowej osoby**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-229">Click **New Person**.</span></span> 
4. <span data-ttu-id="7c4df-230">W oknie dialogowym nowej osoby wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7c4df-230">On the New Person dialog, perform the following steps:</span></span>
   
    ![Utwórz @Task użytkownika testowego][21] 
   
    <span data-ttu-id="7c4df-232">a.</span><span class="sxs-lookup"><span data-stu-id="7c4df-232">a.</span></span> <span data-ttu-id="7c4df-233">W **imię** tekstowym, wpisz "Britta".</span><span class="sxs-lookup"><span data-stu-id="7c4df-233">In the **First Name** textbox, type "Britta".</span></span>
   
    <span data-ttu-id="7c4df-234">b.</span><span class="sxs-lookup"><span data-stu-id="7c4df-234">b.</span></span> <span data-ttu-id="7c4df-235">W **nazwisko** tekstowym, wpisz "Simona".</span><span class="sxs-lookup"><span data-stu-id="7c4df-235">In the **Last Name** textbox, type "Simon".</span></span>
   
    <span data-ttu-id="7c4df-236">c.</span><span class="sxs-lookup"><span data-stu-id="7c4df-236">c.</span></span> <span data-ttu-id="7c4df-237">W **adres E-mail** tekstowym, wpisz adres e-mail Simona Britta w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7c4df-237">In the **Email Address** textbox, type Britta Simon's email address in Azure Active Directory.</span></span>
   
    <span data-ttu-id="7c4df-238">d.</span><span class="sxs-lookup"><span data-stu-id="7c4df-238">d.</span></span> <span data-ttu-id="7c4df-239">Kliknij przycisk **Dodaj osobę**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-239">Click **Add Person**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7c4df-240">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="7c4df-240">Assigning the Azure AD test user</span></span>
<span data-ttu-id="7c4df-241">Celem tej sekcji jest włączenie Simona Britta do używania Azure logowania jednokrotnego za udostępnienie jej @Task.</span><span class="sxs-lookup"><span data-stu-id="7c4df-241">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to @Task.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="7c4df-243">**Aby przypisać Simona Britta do @Task, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="7c4df-243">**To assign Britta Simon to @Task, perform the following steps:**</span></span>

1. <span data-ttu-id="7c4df-244">W klasycznym portalu Azure, aby otworzyć widok aplikacji, w widoku katalogu, kliknij polecenie **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="7c4df-244">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Przypisz użytkownika][201] 
2. <span data-ttu-id="7c4df-246">Na liście aplikacji zaznacz  **@Task** .</span><span class="sxs-lookup"><span data-stu-id="7c4df-246">In the applications list, select **@Task**.</span></span>
   
    ![Przypisz użytkownika][202] 
3. <span data-ttu-id="7c4df-248">W menu u góry kliknij **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-248">In the menu on the top, click **Users**.</span></span>
   
    ![Przypisz użytkownika][203] 
4. <span data-ttu-id="7c4df-250">Na liście użytkowników wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-250">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="7c4df-251">Na pasku narzędzi u dołu, kliknij przycisk **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="7c4df-251">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Przypisz użytkownika][205]

### <a name="testing-single-sign-on"></a><span data-ttu-id="7c4df-253">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="7c4df-253">Testing Single Sign-On</span></span>
<span data-ttu-id="7c4df-254">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="7c4df-254">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="7c4df-255">Po kliknięciu @Task kafelka w panelu dostępu, należy pobrać automatycznie zalogowane do Twojej @Task aplikacji.</span><span class="sxs-lookup"><span data-stu-id="7c4df-255">When you click the @Task tile in the Access Panel, you should get automatically signed-on to your @Task application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7c4df-256">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="7c4df-256">Additional Resources</span></span>
* [<span data-ttu-id="7c4df-257">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7c4df-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7c4df-258">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7c4df-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-attask-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-attask-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-attask-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-attask-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_01.png
[30]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_02.png


[6]: ./media/active-directory-saas-attask-tutorial/tutorial_general_05.png
[7]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_03.png
[8]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_04.png
[9]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_05.png
[10]: ./media/active-directory-saas-attask-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-attask-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-attask-tutorial/tutorial_general_100.png
[21]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_08.png


[23]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_06.png

[200]: ./media/active-directory-saas-attask-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-attask-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-attask-tutorial/tutorial_attask_09.png
[203]: ./media/active-directory-saas-attask-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-attask-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-attask-tutorial/tutorial_general_205.png






