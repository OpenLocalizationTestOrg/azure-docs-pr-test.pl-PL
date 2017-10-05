---
title: 'Samouczek: Integracji Azure Active Directory z Bynder | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Bynder."
services: active-directory
documentationcenter: 
author: jeevansd
manager: femila
editor: 
ms.assetid: 4fb0ab26-b3b9-420a-8072-a0be80ea021e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: jeedes
ms.openlocfilehash: 6786d7eb6a11405278ef7267f25279f9e39b3bde
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bynder"></a><span data-ttu-id="a033c-103">Samouczek: Integracji Azure Active Directory z Bynder</span><span class="sxs-lookup"><span data-stu-id="a033c-103">Tutorial: Azure Active Directory integration with Bynder</span></span>
<span data-ttu-id="a033c-104">Celem tego samouczka jest pokazanie sposobu integracji Bynder z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a033c-104">The objective of this tutorial is to show you how to integrate Bynder with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a033c-105">Integracja z usługą Azure AD Bynder zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="a033c-105">Integrating Bynder with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="a033c-106">Można kontrolować w usłudze Azure AD, który ma dostęp do Bynder</span><span class="sxs-lookup"><span data-stu-id="a033c-106">You can control in Azure AD who has access to Bynder</span></span>
* <span data-ttu-id="a033c-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do Bynder rejestracji jednokrotnej (SSO) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a033c-107">You can enable your users to automatically get signed-on to Bynder single sign-on (SSO) with their Azure AD accounts</span></span>
* <span data-ttu-id="a033c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="a033c-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="a033c-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a033c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a033c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a033c-110">Prerequisites</span></span>
<span data-ttu-id="a033c-111">Aby skonfigurować integrację usługi Azure AD z Bynder, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="a033c-111">To configure Azure AD integration with Bynder, you need the following items:</span></span>

* <span data-ttu-id="a033c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a033c-112">An Azure AD subscription</span></span>
* <span data-ttu-id="a033c-113">Subskrypcja włączone Bynder jednokrotnego (SSO)</span><span class="sxs-lookup"><span data-stu-id="a033c-113">A Bynder single-sign on (SSO) enabled subscription</span></span>

>[!NOTE]
><span data-ttu-id="a033c-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="a033c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span> 
> 

<span data-ttu-id="a033c-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="a033c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="a033c-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="a033c-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="a033c-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać [miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a033c-117">If you don't have an Azure AD trial environment, you can get a [one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a033c-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="a033c-118">Scenario description</span></span>
<span data-ttu-id="a033c-119">Celem tego samouczka jest umożliwienie testowania Usługa rejestracji Jednokrotnej w Microsoft Azure AD w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="a033c-119">The objective of this tutorial is to enable you to test Microsoft Azure AD SSO in a test environment.</span></span>

<span data-ttu-id="a033c-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="a033c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a033c-121">Dodawanie Bynder z galerii</span><span class="sxs-lookup"><span data-stu-id="a033c-121">Adding Bynder from the gallery</span></span>
2. <span data-ttu-id="a033c-122">Konfigurowanie i testowania Usługa rejestracji Jednokrotnej w Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="a033c-122">Configuring and testing Microsoft Azure AD SSO</span></span>

## <a name="add-bynder-from-the-gallery"></a><span data-ttu-id="a033c-123">Dodaj Bynder z galerii</span><span class="sxs-lookup"><span data-stu-id="a033c-123">Add Bynder from the gallery</span></span>
<span data-ttu-id="a033c-124">Aby skonfigurować integrację usługi Azure AD Bynder, należy dodać Bynder z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="a033c-124">To configure the integration of Bynder into Azure AD, you need to add Bynder from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a033c-125">**Aby dodać Bynder z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a033c-125">**To add Bynder from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a033c-126">W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a033c-126">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Usługa Active Directory][1]
2. <span data-ttu-id="a033c-128">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="a033c-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="a033c-129">Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="a033c-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Aplikacje][2]
4. <span data-ttu-id="a033c-131">Kliknij przycisk **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="a033c-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplikacje][3]
5. <span data-ttu-id="a033c-133">Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.</span><span class="sxs-lookup"><span data-stu-id="a033c-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Aplikacje][4]
6. <span data-ttu-id="a033c-135">W polu wyszukiwania wpisz **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="a033c-135">In the search box, type **Bynder**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_01.png)
7. <span data-ttu-id="a033c-137">W panelu wyników wybierz **Bynder**, a następnie kliknij przycisk **Complete** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="a033c-137">In the results panel, select **Bynder**, and then click **Complete** to add the application.</span></span>
   
    ![Wybieranie aplikacji w galerii](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_001.png)

## <a name="configure-and-test-microsoft-azure-ad-sso"></a><span data-ttu-id="a033c-139">Konfiguracja i testowanie Usługa rejestracji Jednokrotnej w Microsoft Azure AD</span><span class="sxs-lookup"><span data-stu-id="a033c-139">Configure and test Microsoft Azure AD SSO</span></span>
<span data-ttu-id="a033c-140">Jest celem tej sekcji opisano sposób konfigurowania i testowania programu Microsoft Azure AD usługa rejestracji Jednokrotnej z Bynder w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="a033c-140">The objective of this section is to show you how to configure and test Microsoft Azure AD SSO with Bynder based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a033c-141">Dla logowania jednokrotnego do pracy usługi Azure AD musi wiedzieć, co to jest odpowiednikiem użytkownikowi w Bynder użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a033c-141">For SSO to work, Azure AD needs to know what the counterpart user in Bynder to an user in Azure AD is.</span></span> <span data-ttu-id="a033c-142">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w Bynder musi się.</span><span class="sxs-lookup"><span data-stu-id="a033c-142">In other words, a link relationship between an Azure AD user and the related user in Bynder needs to be established.</span></span>

<span data-ttu-id="a033c-143">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w Bynder.</span><span class="sxs-lookup"><span data-stu-id="a033c-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Bynder.</span></span>

<span data-ttu-id="a033c-144">Aby skonfigurować i przetestować programu Microsoft Azure AD usługa rejestracji Jednokrotnej z Bynder, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="a033c-144">To configure and test Microsoft Azure AD SSO with Bynder, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a033c-145">**[Konfigurowanie usługi Microsoft Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="a033c-145">**[Configuring Microsoft Azure AD single sign-on](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a033c-146">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Microsoft Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a033c-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Microsoft Azure AD Single Sign-On with Britta Simon.</span></span>
3. <span data-ttu-id="a033c-147">**[Tworzenie użytkownika testowego Bynder](#creating-a-bynder-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Bynder połączonego z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a033c-147">**[Creating a Bynder test user](#creating-a-bynder-test-user)** - to have a counterpart of Britta Simon in Bynder that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="a033c-148">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Microsoft Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="a033c-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Microsoft Azure AD Single Sign-On.</span></span>
5. <span data-ttu-id="a033c-149">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="a033c-149">**[Testing single sign-on](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-microsoft-azure-ad-sso"></a><span data-ttu-id="a033c-150">Konfigurowanie logowania jednokrotnego usługi AD platformy Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="a033c-150">Configuring Microsoft Azure AD SSO</span></span>
<span data-ttu-id="a033c-151">W tej sekcji można włączyć Usługa rejestracji Jednokrotnej w Microsoft Azure AD w klasycznym portalu i skonfigurować logowanie Jednokrotne w aplikacji Bynder.</span><span class="sxs-lookup"><span data-stu-id="a033c-151">In this section, you enable Microsoft Azure AD SSO in the classic portal and configure SSO in your Bynder application.</span></span>

<span data-ttu-id="a033c-152">**Aby skonfigurować Usługa rejestracji Jednokrotnej w Microsoft Azure AD z Bynder, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a033c-152">**To configure Microsoft Azure AD SSO with Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="a033c-153">W klasycznym portalu na **Bynder** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować logowanie jednokrotne** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="a033c-153">In the classic portal, on the **Bynder** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][6] 
2. <span data-ttu-id="a033c-155">Na **jak chcesz użytkownikom zalogować się na Bynder** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="a033c-155">On the **How would you like users to sign on to Bynder** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_03.png)
3. <span data-ttu-id="a033c-157">Na **Konfigurowanie ustawień aplikacji** strony okna dialogowego, jeśli chcesz skonfigurować aplikację w **IDP zainicjował tryb**, wykonaj następujące kroki i kliknij przycisk **dalej**:</span><span class="sxs-lookup"><span data-stu-id="a033c-157">On the **Configure App Settings** dialog page, If you wish to configure the application in **IDP initiated mode**, perform the following steps and click **Next**:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_04.png)
  1. <span data-ttu-id="a033c-159">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.getbynder.com/sso/SAML/authenticate/`</span><span class="sxs-lookup"><span data-stu-id="a033c-159">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/sso/SAML/authenticate/`</span></span>
  2. <span data-ttu-id="a033c-160">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="a033c-160">Click **Next**.</span></span>
4. <span data-ttu-id="a033c-161">Jeśli chcesz skonfigurować aplikację w **SP zainicjował tryb** na **Konfigurowanie ustawień aplikacji** strony okna dialogowego, a następnie kliknij polecenie **"Pokaż zaawansowane ustawienia (opcjonalnie)"** , a następnie wprowadź **na adres URL logowania** i kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="a033c-161">If you wish to configure the application in **SP initiated mode** on the **Configure App Settings** dialog page, then click on the **“Show advanced settings (optional)”** and then enter the **Sign On URL** and click **Next**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_10.png)
  1. <span data-ttu-id="a033c-163">W **na adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<company name>.getbynder.com/login/`</span><span class="sxs-lookup"><span data-stu-id="a033c-163">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<company name>.getbynder.com/login/`</span></span>
  2. <span data-ttu-id="a033c-164">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="a033c-164">Click **Next**.</span></span>
  
   >[!NOTE]
   ><span data-ttu-id="a033c-165">Wartość na adres URL logowania w tym samouczku jest po prostu placeholfer.</span><span class="sxs-lookup"><span data-stu-id="a033c-165">The value for the Sign On URL in this tutorial is just a placeholfer.</span></span> <span data-ttu-id="a033c-166">Aby uzyskać rzeczywiste vlaue dla danego środowiska, skontaktuj się z Bynder.</span><span class="sxs-lookup"><span data-stu-id="a033c-166">To get the actual vlaue for your environment, contact Bynder.</span></span>
   >

5. <span data-ttu-id="a033c-167">Na **skonfigurować logowanie jednokrotne w Bynder** , wykonaj poniższe kroki, a następnie kliknij przycisk **dalej**:</span><span class="sxs-lookup"><span data-stu-id="a033c-167">On the **Configure single sign-on at Bynder** page, perform the following steps and click **Next**:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_05.png)  
  1. <span data-ttu-id="a033c-169">Kliknij przycisk **pobierania metadanych**, a następnie zapisz plik na komputerze.</span><span class="sxs-lookup"><span data-stu-id="a033c-169">Click **Download metadata**, and then save the file on your computer.</span></span>
  2. <span data-ttu-id="a033c-170">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="a033c-170">Click **Next**.</span></span>
6. <span data-ttu-id="a033c-171">Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z zespołem pomocy technicznej Bynder.</span><span class="sxs-lookup"><span data-stu-id="a033c-171">To get SSO configured for your application, contact your Bynder support team.</span></span> <span data-ttu-id="a033c-172">Dołącz plik metadanych pobranych i udostępniać je zespołowi Bynder konfigurowania rejestracji Jednokrotnej w bok.</span><span class="sxs-lookup"><span data-stu-id="a033c-172">Attach the downloaded metadata file and share it with Bynder team to set up SSO on their side.</span></span>
7. <span data-ttu-id="a033c-173">W klasycznym portalu, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="a033c-173">In the classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>
   
    ![Azure AD rejestracji jednokrotnej][10]
8. <span data-ttu-id="a033c-175">Na **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="a033c-175">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
   
    ![Azure AD rejestracji jednokrotnej][11]

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="a033c-177">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a033c-177">Create an Azure AD test user</span></span>
<span data-ttu-id="a033c-178">Celem tej sekcji jest tworzenie użytkownika testowego w klasycznym portalu o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="a033c-178">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][20]

<span data-ttu-id="a033c-180">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a033c-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a033c-181">W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a033c-181">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_09.png)
2. <span data-ttu-id="a033c-183">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="a033c-183">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="a033c-184">Aby wyświetlić listę użytkowników, w menu u góry, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="a033c-184">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_03.png)
4. <span data-ttu-id="a033c-186">Aby otworzyć **Dodaj użytkownika** okna dialogowego na pasku narzędzi u dołu, kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="a033c-186">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_04.png)
5. <span data-ttu-id="a033c-188">Na **Poinformuj nas o tym użytkowniku** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a033c-188">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_05.png)
  1. <span data-ttu-id="a033c-190">Jako typ użytkownika wybierz nowego użytkownika w organizacji.</span><span class="sxs-lookup"><span data-stu-id="a033c-190">As Type Of User, select New user in your organization.</span></span>
  2. <span data-ttu-id="a033c-191">W nazwie użytkownika **pole tekstowe**, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a033c-191">In the User Name **textbox**, type **BrittaSimon**.</span></span>
  3. <span data-ttu-id="a033c-192">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="a033c-192">Click **Next**.</span></span>
6. <span data-ttu-id="a033c-193">Na **profilu użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a033c-193">On the **User Profile** dialog page, perform the following steps:</span></span>
   
   ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_06.png)
  1. <span data-ttu-id="a033c-195">W **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="a033c-195">In the **First Name** textbox, type **Britta**.</span></span>  
  2. <span data-ttu-id="a033c-196">W **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="a033c-196">In the **Last Name** textbox, type, **Simon**.</span></span> 
  3. <span data-ttu-id="a033c-197">W **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="a033c-197">In the **Display Name** textbox, type **Britta Simon**.</span></span>
  4. <span data-ttu-id="a033c-198">W **roli** listy, wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="a033c-198">In the **Role** list, select **User**.</span></span>
  5. <span data-ttu-id="a033c-199">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="a033c-199">Click **Next**.</span></span>
7. <span data-ttu-id="a033c-200">Na **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="a033c-200">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_07.png)
8. <span data-ttu-id="a033c-202">Na **Uzyskaj hasło tymczasowe** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="a033c-202">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-bynder-tutorial/create_aaduser_08.png)
   1. <span data-ttu-id="a033c-204">Zanotuj wartość **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="a033c-204">Write down the value of the **New Password**.</span></span>
   2. <span data-ttu-id="a033c-205">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="a033c-205">Click **Complete**.</span></span>   

### <a name="create-a-bynder-test-user"></a><span data-ttu-id="a033c-206">Tworzenie użytkownika testowego Bynder</span><span class="sxs-lookup"><span data-stu-id="a033c-206">Create a Bynder test user</span></span>
<span data-ttu-id="a033c-207">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w Bynder.</span><span class="sxs-lookup"><span data-stu-id="a033c-207">The objective of this section is to create a user called Britta Simon in Bynder.</span></span> <span data-ttu-id="a033c-208">Bynder obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="a033c-208">Bynder supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="a033c-209">Nie ma elementu akcji można w tej sekcji.</span><span class="sxs-lookup"><span data-stu-id="a033c-209">There is no action item for you in this section.</span></span> <span data-ttu-id="a033c-210">Nowy użytkownik zostanie utworzony podczas próby dostępu Bynder, jeśli go jeszcze nie istnieje.</span><span class="sxs-lookup"><span data-stu-id="a033c-210">A new user will be created during an attempt to access Bynder if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="a033c-211">Jeśli trzeba ręcznie utworzyć użytkownika, należy skontaktować się z zespołem pomocy technicznej Bynder.</span><span class="sxs-lookup"><span data-stu-id="a033c-211">If you need to create an user manually, you need to contact the Bynder support team.</span></span> 
> 

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="a033c-212">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="a033c-212">Assign the Azure AD test user</span></span>
<span data-ttu-id="a033c-213">Celem tej sekcji jest włączenie Simona Britta do udostępnienia jej Bynder za pomocą logowania jednokrotnego Azure.</span><span class="sxs-lookup"><span data-stu-id="a033c-213">The objective of this section is to enabling Britta Simon to use Azure SSO by granting her access to Bynder.</span></span>

   ![Przypisz użytkownika][200]

<span data-ttu-id="a033c-215">**Aby przypisać Simona Britta Bynder, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="a033c-215">**To assign Britta Simon to Bynder, perform the following steps:**</span></span>

1. <span data-ttu-id="a033c-216">W klasycznym portalu, aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="a033c-216">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Przypisz użytkownika][201]
2. <span data-ttu-id="a033c-218">Na liście aplikacji zaznacz **Bynder**.</span><span class="sxs-lookup"><span data-stu-id="a033c-218">In the applications list, select **Bynder**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-bynder-tutorial/tutorial_bynder_50.png)
3. <span data-ttu-id="a033c-220">W menu u góry kliknij **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="a033c-220">In the menu on the top, click **Users**.</span></span>
   
    ![Przypisz użytkownika][203]
4. <span data-ttu-id="a033c-222">Na liście użytkowników wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="a033c-222">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="a033c-223">Na pasku narzędzi u dołu, kliknij przycisk **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="a033c-223">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Przypisz użytkownika][205]

### <a name="test-single-sign-on"></a><span data-ttu-id="a033c-225">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="a033c-225">Test single sign-on</span></span>
<span data-ttu-id="a033c-226">Celem tej sekcji służy do testowania konfiguracji Usługa rejestracji Jednokrotnej w Microsoft Azure AD za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="a033c-226">The objective of this section is to test your Microsoft Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="a033c-227">Po kliknięciu kafelka Bynder w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji Bynder.</span><span class="sxs-lookup"><span data-stu-id="a033c-227">When you click the Bynder tile in the Access Panel, you should get automatically signed-on to your Bynder application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a033c-228">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="a033c-228">Additional resources</span></span>
* [<span data-ttu-id="a033c-229">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a033c-229">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a033c-230">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a033c-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-bynder-tutorial/tutorial_general_205.png
