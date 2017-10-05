---
title: 'Samouczek: Integracji Azure Active Directory z miejsca pracy Soonr | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i Soonr w miejscu pracy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
editor: na
ms.assetid: b75f5f00-ea8b-4850-ae2e-134e5d678d97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 76946e4af624d70f2202601ee935523ca3db4314
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-soonr-workplace"></a><span data-ttu-id="cf6c6-103">Samouczek: Integracji Azure Active Directory z Soonr w miejscu pracy</span><span class="sxs-lookup"><span data-stu-id="cf6c6-103">Tutorial: Azure Active Directory integration with Soonr Workplace</span></span>

<span data-ttu-id="cf6c6-104">Celem tego samouczka jest pokazanie sposobu integracji Soonr miejsca pracy z usługą Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cf6c6-104">The objective of this tutorial is to show you how to integrate Soonr Workplace with Azure Active Directory (Azure AD).</span></span>  
<span data-ttu-id="cf6c6-105">Integrowanie Soonr miejsca pracy z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="cf6c6-105">Integrating Soonr Workplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cf6c6-106">Można kontrolować w usłudze Azure AD, który ma dostęp do miejsca pracy Soonr</span><span class="sxs-lookup"><span data-stu-id="cf6c6-106">You can control in Azure AD who has access to Soonr Workplace</span></span>
- <span data-ttu-id="cf6c6-107">Umożliwia użytkownikom automatycznie pobrać zalogowane Soonr w miejscu pracy (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf6c6-107">You can enable your users to automatically get signed-on to Soonr Workplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cf6c6-108">Możesz zarządzać kont w jednej centralnej lokalizacji - klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="cf6c6-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="cf6c6-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cf6c6-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf6c6-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="cf6c6-110">Prerequisites</span></span>

<span data-ttu-id="cf6c6-111">Aby skonfigurować integrację usługi Azure AD z miejsca pracy Soonr, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="cf6c6-111">To configure Azure AD integration with Soonr Workplace, you need the following items:</span></span>

- <span data-ttu-id="cf6c6-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf6c6-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cf6c6-113">Obszar roboczy Soonr jednokrotnego włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="cf6c6-113">A Soonr Workplace single-sign on enabled subscription</span></span>


> [!NOTE] 
> <span data-ttu-id="cf6c6-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="cf6c6-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="cf6c6-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cf6c6-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="cf6c6-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cf6c6-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="cf6c6-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="cf6c6-118">Scenario description</span></span>
<span data-ttu-id="cf6c6-119">Celem tego samouczka jest umożliwienie umożliwia testowanie usługi Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>  
<span data-ttu-id="cf6c6-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="cf6c6-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cf6c6-121">Dodawanie miejsca pracy Soonr z galerii</span><span class="sxs-lookup"><span data-stu-id="cf6c6-121">Adding Soonr Workplace from the gallery</span></span>
2. <span data-ttu-id="cf6c6-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="cf6c6-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-soonr-workplace-from-the-gallery"></a><span data-ttu-id="cf6c6-123">Dodawanie miejsca pracy Soonr z galerii</span><span class="sxs-lookup"><span data-stu-id="cf6c6-123">Adding Soonr Workplace from the gallery</span></span>
<span data-ttu-id="cf6c6-124">Aby skonfigurować integrację usługi Azure AD Soonr w miejscu pracy, należy dodać Soonr miejsca pracy z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-124">To configure the integration of Soonr Workplace into Azure AD, you need to add Soonr Workplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cf6c6-125">**Aby dodać miejsce pracy Soonr z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="cf6c6-125">**To add Soonr Workplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cf6c6-126">W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-126">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="cf6c6-128">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="cf6c6-129">Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Aplikacje][2]

4. <span data-ttu-id="cf6c6-131">Kliknij przycisk **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-131">Click **Add** at the bottom of the page.</span></span>

    ![Aplikacje][3]

5. <span data-ttu-id="cf6c6-133">Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
 
    ![Aplikacje][4]

6. <span data-ttu-id="cf6c6-135">W polu wyszukiwania wpisz **pracy Soonr**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-135">In the search box, type **Soonr Workplace**.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_01.png)

7. <span data-ttu-id="cf6c6-137">W okienku wyników wybierz **pracy Soonr**, a następnie kliknij przycisk **Complete** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-137">In the results pane, select **Soonr Workplace**, and then click **Complete** to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_02.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cf6c6-139">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="cf6c6-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cf6c6-140">Celem tej sekcji jest, jak skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z Soonr w miejscu pracy na podstawie użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="cf6c6-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with Soonr Workplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="cf6c6-141">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, co jest odpowiednikiem użytkownikowi w miejscu pracy Soonr użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-141">For single sign-on to work, Azure AD needs to know what the counterpart user in Soonr Workplace to an user in Azure AD is.</span></span> <span data-ttu-id="cf6c6-142">Innymi słowy relację łącza między użytkownika usługi Azure AD i danemu użytkownikowi w miejscu pracy Soonr musi określone.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-142">In other words, a link relationship between an Azure AD user and the related user in Soonr Workplace needs to be established.</span></span>  

<span data-ttu-id="cf6c6-143">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w miejscu pracy Soonr.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Soonr Workplace.</span></span>

<span data-ttu-id="cf6c6-144">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z miejsca pracy Soonr, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="cf6c6-144">To configure and test Azure AD single sign-on with Soonr Workplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cf6c6-145">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cf6c6-146">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cf6c6-147">**[Tworzenie użytkownika testowego pracy Soonr](#creating-a-soonr-workplace-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta Soonr miejsca pracy, połączonej z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-147">**[Creating a Soonr Workplace test user](#creating-a-soonr-workplace-test-user)** - to have a counterpart of Britta Simon in Soonr Workplace that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="cf6c6-148">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cf6c6-149">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cf6c6-150">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="cf6c6-150">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cf6c6-151">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w klasycznym portalu i skonfigurować logowanie jednokrotne w miejscu pracy Soonr aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your Soonr Workplace application.</span></span>


<span data-ttu-id="cf6c6-152">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z miejsca pracy Soonr, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="cf6c6-152">**To configure Azure AD single sign-on with Soonr Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="cf6c6-153">W klasycznym portalu Azure na **Soonr pracy** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować logowanie jednokrotne** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-153">In the Azure classic portal, on the **Soonr Workplace** application integration page, click **Configure single sign-on** to open the **Configure Single Sign-On**  dialog.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][6] 

2. <span data-ttu-id="cf6c6-155">Na **jak chcesz użytkownikom zalogować do miejsca pracy Soonr** wybierz pozycję **Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-155">On the **How would you like users to sign on to Soonr Workplace** page, select **Azure AD Single Sign-On**, and then click **Next**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_03.png) 

3. <span data-ttu-id="cf6c6-157">Na **Konfigurowanie ustawień aplikacji** okna dialogowego wykonaj następujące kroki:.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-157">On the **Configure App Settings** dialog page, perform the following steps:.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_04.png) 

    <span data-ttu-id="cf6c6-159">a.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-159">a.</span></span> <span data-ttu-id="cf6c6-160">W **na adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-160">In the **Sign On URL** textbox, type a URL using the following pattern: `https://<server-name>.soonr.com/singlesignon/saml/SSO`.</span></span>

    <span data-ttu-id="cf6c6-161">b.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-161">b.</span></span> <span data-ttu-id="cf6c6-162">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-162">Click **Next**.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="cf6c6-163">Należy pamiętać, że nie jest rzeczywistą wartość.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-163">Please note that this is not the real value.</span></span> <span data-ttu-id="cf6c6-164">Należy zaktualizować tę wartość rzeczywista logowania na adres URL.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-164">You have to update this value with the actual Sign On URL.</span></span> <span data-ttu-id="cf6c6-165">Skontaktuj się z zespołem pomocy technicznej Soonr w miejscu pracy, aby zyskać tę wartość.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-165">Contact Soonr Workplace support team to get this value.</span></span>

4. <span data-ttu-id="cf6c6-166">Na **skonfigurować logowanie jednokrotne w miejscu pracy Soonr** kliknij przycisk **pobierania metadanych** , a następnie zapisz plik na komputerze:</span><span class="sxs-lookup"><span data-stu-id="cf6c6-166">On the **Configure single sign-on at Soonr Workplace** page, click **Download metadata** and then save the file on your computer:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_05.png) 

5. <span data-ttu-id="cf6c6-168">Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, skontaktuj się z zespołem pomocy technicznej Soonr w miejscu pracy i podaj następujące:</span><span class="sxs-lookup"><span data-stu-id="cf6c6-168">To get SSO configured for your application, contact your Soonr Workplace support team and provide them with the following:</span></span> 

    <span data-ttu-id="cf6c6-169">• Pobrany **metadanych** pliku</span><span class="sxs-lookup"><span data-stu-id="cf6c6-169">•  The downloaded **Metadata** file</span></span>

    <span data-ttu-id="cf6c6-170">• **Adres URL wystawcy**</span><span class="sxs-lookup"><span data-stu-id="cf6c6-170">•  The **Issuer URL**</span></span>

    <span data-ttu-id="cf6c6-171">• **Adres URL logowania jednokrotnego SAML**</span><span class="sxs-lookup"><span data-stu-id="cf6c6-171">•  The **SAML SSO URL**</span></span>

    <span data-ttu-id="cf6c6-172">• **Pojedynczy adres URL wylogowania usługi**</span><span class="sxs-lookup"><span data-stu-id="cf6c6-172">•  The **Single Sign-Out Service URL**</span></span>

    >[!NOTE]
    ><span data-ttu-id="cf6c6-173">Ta aplikacja została zastąpiona nowszą <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">pracy Autotask</a> i może odnosić się <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">to</a> samouczka do konfigurowania aplikacji z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-173">This application is superseded by <a href="https://azure.microsoft.com/en-us/marketplace/partners/autotask-corporataion/autotask/">Autotask Workplace</a> and you can refer <a href="https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-autotaskworkplace-tutorial">this</a> tutorial for configuring the application with Azure AD.</span></span>
   
6. <span data-ttu-id="cf6c6-174">W klasycznym portalu Azure, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-174">In the Azure classic portal, select the single sign-on configuration confirmation, and then click **Next**.</span></span>

    ![Azure AD rejestracji jednokrotnej][10]

7. <span data-ttu-id="cf6c6-176">Na **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-176">On the **Single sign-on confirmation** page, click **Complete**.</span></span>  
  
    ![Azure AD rejestracji jednokrotnej][11]



### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cf6c6-178">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf6c6-178">Creating an Azure AD test user</span></span>
<span data-ttu-id="cf6c6-179">Celem tej sekcji jest tworzenie użytkownika testowego w klasycznym portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-179">The objective of this section is to create a test user in the Azure classic portal called Britta Simon.</span></span>  

![Tworzenie użytkowników usługi Azure AD][20]

<span data-ttu-id="cf6c6-181">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="cf6c6-181">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cf6c6-182">W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-182">In the **Azure classic portal**, on the left navigation pane, click **Active Directory**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_09.png) 

2. <span data-ttu-id="cf6c6-184">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-184">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>

3. <span data-ttu-id="cf6c6-185">Aby wyświetlić listę użytkowników, w menu u góry, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-185">To display the list of users, in the menu on the top, click **Users**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cf6c6-187">Aby otworzyć **Dodaj użytkownika** okna dialogowego na pasku narzędzi u dołu, kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-187">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_04.png) 

5. <span data-ttu-id="cf6c6-189">Na **Poinformuj nas o tym użytkowniku** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cf6c6-189">On the **Tell us about this user** dialog page, perform the following steps:</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_05.png) 

    <span data-ttu-id="cf6c6-191">a.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-191">a.</span></span> <span data-ttu-id="cf6c6-192">Jako typ użytkownika wybierz nowego użytkownika w organizacji.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-192">As Type Of User, select New user in your organization.</span></span>

    <span data-ttu-id="cf6c6-193">b.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-193">b.</span></span> <span data-ttu-id="cf6c6-194">W nazwie użytkownika **pole tekstowe**, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-194">In the User Name **textbox**, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cf6c6-195">c.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-195">c.</span></span> <span data-ttu-id="cf6c6-196">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-196">Click **Next**.</span></span>

6.  <span data-ttu-id="cf6c6-197">Na **profilu użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cf6c6-197">On the **User Profile** dialog page, perform the following steps:</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_06.png) 

    <span data-ttu-id="cf6c6-199">a.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-199">a.</span></span> <span data-ttu-id="cf6c6-200">W **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-200">In the **First Name** textbox, type **Britta**.</span></span>  

    <span data-ttu-id="cf6c6-201">b.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-201">b.</span></span> <span data-ttu-id="cf6c6-202">W **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-202">In the **Last Name** textbox, type, **Simon**.</span></span>

    <span data-ttu-id="cf6c6-203">c.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-203">c.</span></span> <span data-ttu-id="cf6c6-204">W **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-204">In the **Display Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="cf6c6-205">d.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-205">d.</span></span> <span data-ttu-id="cf6c6-206">W **roli** listy, wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-206">In the **Role** list, select **User**.</span></span>

    <span data-ttu-id="cf6c6-207">e.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-207">e.</span></span> <span data-ttu-id="cf6c6-208">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-208">Click **Next**.</span></span>

7. <span data-ttu-id="cf6c6-209">Na **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-209">On the **Get temporary password** dialog page, click **create**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_07.png) 

8. <span data-ttu-id="cf6c6-211">Na **Uzyskaj hasło tymczasowe** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="cf6c6-211">On the **Get temporary password** dialog page, perform the following steps:</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-soonr-tutorial/create_aaduser_08.png) 

    <span data-ttu-id="cf6c6-213">a.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-213">a.</span></span> <span data-ttu-id="cf6c6-214">Zanotuj wartość **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-214">Write down the value of the **New Password**.</span></span>

    <span data-ttu-id="cf6c6-215">b.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-215">b.</span></span> <span data-ttu-id="cf6c6-216">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="cf6c6-216">Click **Complete**.</span></span>   



### <a name="creating-a-soonr-workplace-test-user"></a><span data-ttu-id="cf6c6-217">Tworzenie użytkownika testowego Soonr w miejscu pracy</span><span class="sxs-lookup"><span data-stu-id="cf6c6-217">Creating a Soonr Workplace test user</span></span>

<span data-ttu-id="cf6c6-218">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w miejscu pracy Soonr.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-218">The objective of this section is to create a user called Britta Simon in Soonr Workplace.</span></span> <span data-ttu-id="cf6c6-219">Należy skontaktować się z zespołem pomocy technicznej Soonr w miejscu pracy, aby utworzyć użytkownika na platformie.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-219">Please work with Soonr Workplace support team to create a user in the platform.</span></span> <span data-ttu-id="cf6c6-220">Można zwiększyć biletu pomocy technicznej z Soonr z <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">tutaj</a>.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-220">You can raise the support ticket with Soonr from <a href="https://na01.safelinks.protection.outlook.com/?url=http%3A%2F%2Fsoonr.com%2FAWPHelp%2FContent%2F0_HOME%2FSupport_for_End_Clients.htm&data=01%7C01%7Cv-saikra%40microsoft.com%7Ccbb4367ab09b4dacaac408d3eebe3f42%7C72f988bf86f141af91ab2d7cd011db47%7C1&sdata=FB92qtE6m%2Fd8yox7AnL2f1h%2FGXwSkma9x9H8Pz0955M%3D&reserved=0/">here</a>.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cf6c6-221">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf6c6-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cf6c6-222">Celem tej sekcji jest włączenie Simona Britta na udostępnienie jej do miejsca pracy Soonr za pomocą usługi Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-222">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to Soonr Workplace.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="cf6c6-224">**Aby przypisać Simona Britta Soonr w miejscu pracy, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="cf6c6-224">**To assign Britta Simon to Soonr Workplace, perform the following steps:**</span></span>

1. <span data-ttu-id="cf6c6-225">W klasycznym portalu Azure, aby otworzyć widok aplikacji, w widoku katalogu, kliknij polecenie **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-225">On the Azure classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="cf6c6-227">Na liście aplikacji zaznacz **pracy Soonr**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-227">In the applications list, select **Soonr Workplace**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-soonr-tutorial/tutorial_soonr_50.png) 

1. <span data-ttu-id="cf6c6-229">W menu u góry kliknij **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-229">In the menu on the top, click **Users**.</span></span>

    ![Przypisz użytkownika][203] 

1. <span data-ttu-id="cf6c6-231">Na liście użytkowników wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-231">In the Users list, select **Britta Simon**.</span></span>

2. <span data-ttu-id="cf6c6-232">Na pasku narzędzi u dołu, kliknij przycisk **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-232">In the toolbar on the bottom, click **Assign**.</span></span>

    ![Przypisz użytkownika][205]



### <a name="testing-single-sign-on"></a><span data-ttu-id="cf6c6-234">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="cf6c6-234">Testing single sign-on</span></span>

<span data-ttu-id="cf6c6-235">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="cf6c6-236">Po kliknięciu kafelka Soonr w miejscu pracy, w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do miejsca pracy Soonr aplikacji.</span><span class="sxs-lookup"><span data-stu-id="cf6c6-236">When you click the Soonr Workplace tile in the Access Panel, you should get automatically signed-on to your Soonr Workplace application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="cf6c6-237">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="cf6c6-237">Additional resources</span></span>

* [<span data-ttu-id="cf6c6-238">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cf6c6-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cf6c6-239">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cf6c6-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_04.png

[6]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_05.png
[10]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_06.png
[11]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_07.png
[20]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_201.png
[203]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_203.png
[204]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_204.png
[205]: ./media/active-directory-saas-soonr-tutorial/tutorial_general_205.png
