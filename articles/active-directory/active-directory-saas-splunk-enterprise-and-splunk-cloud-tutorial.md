---
title: "Samouczek: Integracji usługi Azure Active Directory z Splunk przedsiębiorstwa i w chmurze Splunk | Dokumentacja firmy Microsoft"
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługi Azure Active Directory i Splunk Enterprise i Splunk chmury."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 3/09/2017
ms.author: jeedes
ms.openlocfilehash: b78e9b7161207a74880e912241d5e965b353d1c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="d2991-103">Samouczek: Integracji usługi Azure Active Directory z Splunk przedsiębiorstwa i w chmurze Splunk</span><span class="sxs-lookup"><span data-stu-id="d2991-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="d2991-104">Z tego samouczka dowiesz integrowanie Splunk przedsiębiorstwa i w chmurze Splunk z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d2991-104">In this tutorial, you learn how to integrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d2991-105">Integracja z usługą Azure AD Splunk przedsiębiorstwa i w chmurze Splunk zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="d2991-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d2991-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Splunk przedsiębiorstwa i w chmurze Splunk</span><span class="sxs-lookup"><span data-stu-id="d2991-106">You can control in Azure AD who has access to Splunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="d2991-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Splunk przedsiębiorstwa i w chmurze Splunk rejestracji jednokrotnej (SSO) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2991-107">You can enable your users to automatically get signed-on to Splunk Enterprise and Splunk Cloud single sign-on (SSO) with their Azure AD accounts</span></span>
- <span data-ttu-id="d2991-108">Możesz zarządzać kont w jednej centralnej lokalizacji - klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="d2991-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="d2991-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d2991-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d2991-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="d2991-110">Prerequisites</span></span>

<span data-ttu-id="d2991-111">Aby skonfigurować integrację usługi Azure AD z Splunk przedsiębiorstwa i w chmurze Splunk, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="d2991-111">To configure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need the following items:</span></span>

- <span data-ttu-id="d2991-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2991-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d2991-113">Splunk Enterprise lub logowania jednokrotnego chmury Splunk włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="d2991-113">A Splunk Enterprise or Splunk Cloud SSO enabled subscription</span></span>


>[!NOTE]
><span data-ttu-id="d2991-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="d2991-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
>

<span data-ttu-id="d2991-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="d2991-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d2991-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="d2991-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="d2991-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d2991-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="d2991-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="d2991-118">Scenario description</span></span>
<span data-ttu-id="d2991-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="d2991-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="d2991-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="d2991-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d2991-121">Dodawanie Splunk przedsiębiorstwa i w chmurze Splunk z galerii</span><span class="sxs-lookup"><span data-stu-id="d2991-121">Adding Splunk Enterprise and Splunk Cloud from the gallery</span></span>
2. <span data-ttu-id="d2991-122">Konfigurowanie i testowania logowania jednokrotnego programu Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2991-122">Configuring and testing Azure AD SSO</span></span>


## <a name="add-splunk-enterprise-and-splunk-cloud-from-the-gallery"></a><span data-ttu-id="d2991-123">Dodaj Splunk przedsiębiorstwa i w chmurze Splunk z galerii</span><span class="sxs-lookup"><span data-stu-id="d2991-123">Add Splunk Enterprise and Splunk Cloud from the gallery</span></span>
<span data-ttu-id="d2991-124">Aby skonfigurować integrację Splunk przedsiębiorstwa i Splunk chmury do usługi Azure AD, należy dodać Splunk przedsiębiorstwa i w chmurze Splunk z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="d2991-124">To configure the integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need to add Splunk Enterprise and Splunk Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d2991-125">**Aby dodać Splunk przedsiębiorstwa i w chmurze Splunk z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d2991-125">**To add Splunk Enterprise and Splunk Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d2991-126">W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d2991-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Usługa Active Directory][1]

2. <span data-ttu-id="d2991-128">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="d2991-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="d2991-129">Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="d2991-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Aplikacje][2]

4. <span data-ttu-id="d2991-131">Kliknij przycisk **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="d2991-131">Click **Add** at the bottom of the page.</span></span>

    ![Aplikacje][3]

5. <span data-ttu-id="d2991-133">Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.</span><span class="sxs-lookup"><span data-stu-id="d2991-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>

    ![Aplikacje][4]

6. <span data-ttu-id="d2991-135">W polu wyszukiwania wpisz **Splunk przedsiębiorstwa lub w chmurze Splunk**.</span><span class="sxs-lookup"><span data-stu-id="d2991-135">In the search box, type **Splunk Enterprise or Splunk Cloud**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_01.png)

7. <span data-ttu-id="d2991-137">W okienku wyników wybierz **Splunk przedsiębiorstwa i w chmurze Splunk**, a następnie kliknij przycisk **Complete** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="d2991-137">In the results pane, select **Splunk Enterprise and Splunk Cloud**, and then click **Complete** to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_02.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d2991-139">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d2991-139">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="d2991-140">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Splunk przedsiębiorstwa i Splunk chmury oparte na użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="d2991-140">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d2991-141">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w Splunk przedsiębiorstwa i w chmurze Splunk jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2991-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Splunk Enterprise and Splunk Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="d2991-142">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w organizacji Splunk i w chmurze Splunk musi się.</span><span class="sxs-lookup"><span data-stu-id="d2991-142">In other words, a link relationship between an Azure AD user and the related user in Splunk Enterprise and Splunk Cloud needs to be established.</span></span>

<span data-ttu-id="d2991-143">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **nazwy użytkownika** Splunk przedsiębiorstwa i Splunk chmury.</span><span class="sxs-lookup"><span data-stu-id="d2991-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Splunk Enterprise and Splunk Cloud.</span></span>

<span data-ttu-id="d2991-144">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Splunk przedsiębiorstwa i w chmurze Splunk, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="d2991-144">To configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d2991-145">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="d2991-145">**[Configuring Azure AD single sign-on](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d2991-146">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d2991-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d2991-147">**[Tworzenie użytkownika testowego Splunk przedsiębiorstwa i w chmurze Splunk](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)**  — mają odpowiednika Simona Britta w przedsiębiorstwie Splunk i Splunk chmurze, która jest połączona z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d2991-147">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - to have a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="d2991-148">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="d2991-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d2991-149">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="d2991-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d2991-150">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d2991-150">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d2991-151">W tej sekcji włączenia funkcji logowania jednokrotnego usługi Azure AD w klasycznym portalu i konfigurowanie logowania jednokrotnego w aplikacji przedsiębiorstwa Splunk i Splunk chmury.</span><span class="sxs-lookup"><span data-stu-id="d2991-151">In this section, you enable Azure AD SSO in the classic portal and configure SSO in your Splunk Enterprise and Splunk Cloud application.</span></span>


<span data-ttu-id="d2991-152">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z Splunk przedsiębiorstwa i Splunk chmury, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d2991-152">**To configure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="d2991-153">W klasycznym portalu na **Splunk przedsiębiorstwa i w chmurze Splunk** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować logowanie jednokrotne**okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="d2991-153">In the classic portal, on the **Splunk Enterprise and Splunk Cloud** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
     
    ![Konfigurowanie rejestracji jednokrotnej][6] 

2. <span data-ttu-id="d2991-155">Na **jak chcesz użytkownikom logowanie się Splunk przedsiębiorstwa i w chmurze Splunk** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="d2991-155">On the **How would you like users to sign on to Splunk Enterprise and Splunk Cloud** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_03.png) 

3. <span data-ttu-id="d2991-157">Na **Konfigurowanie ustawień aplikacji** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d2991-157">On the **Configure App Settings** dialog page, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_04.png) 
  1. <span data-ttu-id="d2991-159">W **na adres URL logowania** tekstowym, wpisz adres URL używany przez użytkowników do logowania jednokrotnego do aplikacji przedsiębiorstwa Splunk i w chmurze Splunk przy użyciu następującego wzorca:`https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="d2991-159">In the **Sign On URL** textbox, type the URL used by your users to sign-on to your Splunk Enterprise and Splunk Cloud application using the following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
  2. <span data-ttu-id="d2991-160">W **identyfikator** tekstowym, wpisz adres URL serwera Splunk.</span><span class="sxs-lookup"><span data-stu-id="d2991-160">In the **Identifier** textbox, type the URL of your Splunk Server.</span></span>
  3. <span data-ttu-id="d2991-161">W **adres URL odpowiedzi** tekstowym, wpisz adres URL z następującego wzorca:`https://<splunkserver>/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="d2991-161">In the **Reply URL** textbox, type the URL with the following pattern: `https://<splunkserver>/saml/acs`</span></span>
  4. <span data-ttu-id="d2991-162">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="d2991-162">Click **Next**.</span></span>
 
4. <span data-ttu-id="d2991-163">Na **skonfigurować logowanie jednokrotne w Splunk przedsiębiorstwa i w chmurze Splunk** wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d2991-163">On the **Configure single sign-on at Splunk Enterprise and Splunk Cloud** page, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_05.png)
  1. <span data-ttu-id="d2991-165">Kliknij przycisk **pobierania metadanych**, a następnie zapisz plik na komputerze.</span><span class="sxs-lookup"><span data-stu-id="d2991-165">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="d2991-166">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="d2991-166">Click **Next**.</span></span>

5. <span data-ttu-id="d2991-167">Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z Splunk przedsiębiorstwa i Splunk chmury z pomocą techniczną i podaj z następującymi:</span><span class="sxs-lookup"><span data-stu-id="d2991-167">To get SSO configured for your application, contact Splunk Enterprise and Splunk Cloud support team and provide them with the following:</span></span>

    * <span data-ttu-id="d2991-168">Pobrany **federaton metadanych**</span><span class="sxs-lookup"><span data-stu-id="d2991-168">The downloaded **federaton metadata**</span></span>
6. <span data-ttu-id="d2991-169">W klasycznym portalu, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="d2991-169">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
    
    ![Azure AD rejestracji jednokrotnej][10]

7. <span data-ttu-id="d2991-171">Na **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="d2991-171">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
 
    ![Azure AD rejestracji jednokrotnej][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d2991-173">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2991-173">Create an Azure AD test user</span></span>
<span data-ttu-id="d2991-174">W tej sekcji utworzysz użytkownika testowego w klasycznym portalu o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="d2991-174">In this section, you create a test user in the classic portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][20]

<span data-ttu-id="d2991-176">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d2991-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d2991-177">W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d2991-177">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="d2991-179">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="d2991-179">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="d2991-180">Aby wyświetlić listę użytkowników, w menu u góry, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="d2991-180">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d2991-182">Aby otworzyć **Dodaj użytkownika** okna dialogowego na pasku narzędzi u dołu, kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="d2991-182">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="d2991-184">Na **Poinformuj nas o tym użytkowniku** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d2991-184">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_05.png) 
  1. <span data-ttu-id="d2991-186">Jako typ użytkownika wybierz nowego użytkownika w organizacji.</span><span class="sxs-lookup"><span data-stu-id="d2991-186">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="d2991-187">W nazwie użytkownika **pole tekstowe**, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d2991-187">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="d2991-188">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="d2991-188">Click **Next**.</span></span>

6.  <span data-ttu-id="d2991-189">Na **profilu użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d2991-189">On the **User Profile** dialog page, perform the following steps:</span></span>
  
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_06.png) 
  1. <span data-ttu-id="d2991-191">W **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="d2991-191">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="d2991-192">W **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="d2991-192">In the **Last Name** textbox, type, **Simon**.</span></span>
  3. <span data-ttu-id="d2991-193">W **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="d2991-193">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="d2991-194">W **roli** listy, wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="d2991-194">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="d2991-195">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="d2991-195">Click **Next**.</span></span>

7. <span data-ttu-id="d2991-196">Na **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="d2991-196">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="d2991-198">Na **Uzyskaj hasło tymczasowe** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="d2991-198">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/create_aaduser_08.png) 
  1. <span data-ttu-id="d2991-200">Zanotuj wartość **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="d2991-200">Write down the value of the **New Password**.</span></span>
  2. <span data-ttu-id="d2991-201">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="d2991-201">Click **Complete**.</span></span>   

### <a name="create-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="d2991-202">Tworzenie Splunk przedsiębiorstwa i chmury Splunk użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="d2991-202">Create a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="d2991-203">W tej sekcji utworzysz użytkownika o nazwie Simona Britta w przedsiębiorstwie Splunk i Splunk chmury.</span><span class="sxs-lookup"><span data-stu-id="d2991-203">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="d2991-204">Proszę współpracować z Splunk Enterprise i chmury Splunk zespołem pomocy technicznej, aby dodać użytkowników na platformie Splunk przedsiębiorstwa i w chmurze Splunk.</span><span class="sxs-lookup"><span data-stu-id="d2991-204">Please work with Splunk Enterprise and Splunk Cloud support team to add the users in the Splunk Enterprise and Splunk Cloud platform.</span></span>


### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d2991-205">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="d2991-205">Assign the Azure AD test user</span></span>

<span data-ttu-id="d2991-206">W tej sekcji można włączyć Simona Britta umożliwia udostępnienie jej Splunk przedsiębiorstwa i w chmurze Splunk SSOy Azure.</span><span class="sxs-lookup"><span data-stu-id="d2991-206">In this section, you enable Britta Simon to use Azure SSOy granting her access to Splunk Enterprise and Splunk Cloud.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="d2991-208">**Aby przypisać Simona Britta do Splunk przedsiębiorstwa i Splunk chmury, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="d2991-208">**To assign Britta Simon to Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="d2991-209">W klasycznym portalu, aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="d2991-209">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="d2991-211">Na liście aplikacji zaznacz **Splunk przedsiębiorstwa i w chmurze Splunk**.</span><span class="sxs-lookup"><span data-stu-id="d2991-211">In the applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_splunk_50.png) 

3. <span data-ttu-id="d2991-213">W menu u góry kliknij **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="d2991-213">In the menu on the top, click **Users**.</span></span>

    ![Przypisz użytkownika][203]

4. <span data-ttu-id="d2991-215">Na liście użytkowników wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="d2991-215">In the Users list, select **Britta Simon**.</span></span>

5. <span data-ttu-id="d2991-216">Na pasku narzędzi u dołu, kliknij przycisk **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="d2991-216">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Przypisz użytkownika][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="d2991-218">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="d2991-218">Test single sign-on</span></span>

<span data-ttu-id="d2991-219">W tej sekcji można przetestować programu Azure AD SSOonfiguration, za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="d2991-219">In this section, you test your Azure AD SSOonfiguration using the Access Panel.</span></span>

<span data-ttu-id="d2991-220">Po kliknięciu Splunk Enterprise i chmury Splunk kafelka w panelu dostępu, możesz należy pobrać automatycznie zalogowane Splunk przedsiębiorstwa i w chmurze Splunk aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d2991-220">When you click the Splunk Enterprise and Splunk Cloud tile in the Access Panel, you should get automatically signed-on to your Splunk Enterprise and Splunk Cloud application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d2991-221">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="d2991-221">Additional resources</span></span>

* [<span data-ttu-id="d2991-222">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d2991-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d2991-223">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d2991-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-splunk-enterprise-and-splunk-cloud-tutorial/tutorial_general_205.png
