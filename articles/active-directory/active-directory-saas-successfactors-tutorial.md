---
title: 'Samouczek: Integracji Azure Active Directory z SuccessFactors | Dokumentacja firmy Microsoft'
description: "Dowiedz się, jak używać SuccessFactors usłudze Azure Active Directory w celu włączenia logowania jednokrotnego, automatyczne Inicjowanie obsługi i inne!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 32bd8898-c2d2-4aa7-8c46-f1f5c2aa05f1
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/21/2017
ms.author: jeedes
ms.reviewer: jeedes
ms.openlocfilehash: e85a38ccbe25263ac42bc76351416b023fb77c87
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-successfactors"></a><span data-ttu-id="eef8d-103">Samouczek: Integracji Azure Active Directory z SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="eef8d-103">Tutorial: Azure Active Directory integration with SuccessFactors</span></span>
<span data-ttu-id="eef8d-104">Celem tego samouczka jest pokazanie sposobu integracji SuccessFactors z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="eef8d-104">The objective of this tutorial is to show you how to integrate SuccessFactors with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="eef8d-105">Integracja z usługą Azure AD SuccessFactors zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="eef8d-105">Integrating SuccessFactors with Azure AD provides you with the following benefits:</span></span>

* <span data-ttu-id="eef8d-106">Można kontrolować w usłudze Azure AD, który ma dostęp do SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="eef8d-106">You can control in Azure AD who has access to SuccessFactors</span></span>
* <span data-ttu-id="eef8d-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do SuccessFactors (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="eef8d-107">You can enable your users to automatically get signed-on to SuccessFactors (Single Sign-On) with their Azure AD accounts</span></span>
* <span data-ttu-id="eef8d-108">Możesz zarządzać kont w jednej centralnej lokalizacji - klasycznego portalu Azure</span><span class="sxs-lookup"><span data-stu-id="eef8d-108">You can manage your accounts in one central location - the Azure classic portal</span></span>

<span data-ttu-id="eef8d-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="eef8d-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eef8d-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eef8d-110">Prerequisites</span></span>
<span data-ttu-id="eef8d-111">Aby skonfigurować integrację usługi Azure AD z SuccessFactors, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="eef8d-111">To configure Azure AD integration with SuccessFactors, you need the following items:</span></span>

* <span data-ttu-id="eef8d-112">Ważnej subskrypcji platformy Azure</span><span class="sxs-lookup"><span data-stu-id="eef8d-112">A valid Azure subscription</span></span>
* <span data-ttu-id="eef8d-113">Dzierżawcy w SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="eef8d-113">A tenant in SuccessFactors</span></span>

> [!NOTE]
> <span data-ttu-id="eef8d-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="eef8d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>
> 
> 

<span data-ttu-id="eef8d-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="eef8d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

* <span data-ttu-id="eef8d-116">Nie należy używać środowiska produkcyjnego, chyba że jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="eef8d-116">You should not use your production environment, unless this is necessary.</span></span>
* <span data-ttu-id="eef8d-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna [tutaj](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eef8d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="eef8d-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="eef8d-118">Scenario description</span></span>
<span data-ttu-id="eef8d-119">Celem tego samouczka jest umożliwienie umożliwia testowanie usługi Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="eef8d-119">The objective of this tutorial is to enable you to test Azure AD single sign-on in a test environment.</span></span>

<span data-ttu-id="eef8d-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="eef8d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="eef8d-121">Dodawanie SuccessFactors z galerii</span><span class="sxs-lookup"><span data-stu-id="eef8d-121">Adding SuccessFactors from the gallery</span></span>
2. <span data-ttu-id="eef8d-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="eef8d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-successfactors-from-the-gallery"></a><span data-ttu-id="eef8d-123">Dodawanie SuccessFactors z galerii</span><span class="sxs-lookup"><span data-stu-id="eef8d-123">Adding SuccessFactors from the gallery</span></span>
<span data-ttu-id="eef8d-124">Aby skonfigurować integrację usługi Azure AD SuccessFactors, należy dodać SuccessFactors z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="eef8d-124">To configure the integration of SuccessFactors into Azure AD, you need to add SuccessFactors from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="eef8d-125">**Aby dodać SuccessFactors z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="eef8d-125">**To add SuccessFactors from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="eef8d-126">W klasycznym portalu Azure, na panelu nawigacyjnym po lewej stronie kliknij **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-126">In the Azure classic portal, on the left navigation panel, click **Active Directory**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][1]
2. <span data-ttu-id="eef8d-128">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="eef8d-128">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="eef8d-129">Aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="eef8d-129">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][2]
4. <span data-ttu-id="eef8d-131">Kliknij przycisk **Dodaj** w dolnej części strony.</span><span class="sxs-lookup"><span data-stu-id="eef8d-131">Click **Add** at the bottom of the page.</span></span>
   
    ![Aplikacje][3]
5. <span data-ttu-id="eef8d-133">Na **co chcesz zrobić** okna dialogowego, kliknij przycisk **dodać aplikację z galerii**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-133">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][4]
6. <span data-ttu-id="eef8d-135">W **pole wyszukiwania**, typ **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-135">In the **search box**, type **SuccessFactors**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][5]
7. <span data-ttu-id="eef8d-137">W panelu wyników wybierz **SuccessFactors**, a następnie kliknij przycisk **Complete** można dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="eef8d-137">In the results panel, select **SuccessFactors**, and then click **Complete** to add the application.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][6]

## <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="eef8d-139">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="eef8d-139">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="eef8d-140">Jest celem tej sekcji opisano, jak skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SuccessFactors w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="eef8d-140">The objective of this section is to show you how to configure and test Azure AD single sign-on with SuccessFactors based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="eef8d-141">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, co to jest odpowiednikiem użytkownikowi w SuccessFactors użytkownika w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eef8d-141">For single sign-on to work, Azure AD needs to know what the counterpart user in SuccessFactors to an user in Azure AD is.</span></span> <span data-ttu-id="eef8d-142">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w SuccessFactors musi się.</span><span class="sxs-lookup"><span data-stu-id="eef8d-142">In other words, a link relationship between an Azure AD user and the related user in SuccessFactors needs to be established.</span></span>

<span data-ttu-id="eef8d-143">Ta relacja łącza zostanie nawiązane, przypisując wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** w SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="eef8d-143">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in SuccessFactors.</span></span>

<span data-ttu-id="eef8d-144">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SuccessFactors, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="eef8d-144">To configure and test Azure AD single sign-on with SuccessFactors, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="eef8d-145">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="eef8d-145">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="eef8d-146">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="eef8d-146">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="eef8d-147">**[Tworzenie użytkownika testowego SuccessFactors](#creating-a-successfactors-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta SuccessFactors połączonego z jej reprezentacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eef8d-147">**[Creating a SuccessFactors test user](#creating-a-successfactors-test-user)** - to have a counterpart of Britta Simon in SuccessFactors that is linked to the Azure AD representation of her.</span></span>
4. <span data-ttu-id="eef8d-148">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="eef8d-148">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="eef8d-149">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="eef8d-149">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="eef8d-150">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="eef8d-150">Configuring Azure AD single sign-on</span></span>
<span data-ttu-id="eef8d-151">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w klasycznym portalu i skonfigurować logowanie jednokrotne w aplikacji SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="eef8d-151">In this section, you enable Azure AD single sign-on in the classic portal and configure single sign-on in your SuccessFactors application.</span></span>

<span data-ttu-id="eef8d-152">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z SuccessFactors, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="eef8d-152">**To configure Azure AD single sign-on with SuccessFactors, perform the following steps:**</span></span>

1. <span data-ttu-id="eef8d-153">W klasycznym portalu Azure na **SuccessFactors** strona integracji aplikacji, kliknij przycisk **skonfigurować logowanie jednokrotne** otworzyć **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eef8d-153">In the Azure classic portal, on the **SuccessFactors** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][7]
2. <span data-ttu-id="eef8d-155">Na **jak chcesz użytkownikom zalogować się na SuccessFactors** wybierz pozycję **usługi Microsoft Azure AD rejestracji jednokrotnej**, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-155">On the **How would you like users to sign on to SuccessFactors** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][8]
3. <span data-ttu-id="eef8d-157">Na **Konfigurowanie adresu URL aplikacji** , wykonaj następujące czynności, a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-157">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][9]
   
    <span data-ttu-id="eef8d-159">a.</span><span class="sxs-lookup"><span data-stu-id="eef8d-159">a.</span></span> <span data-ttu-id="eef8d-160">W **na adres URL logowania** tekstowym, wpisz adres URL przy użyciu jednej z następujących wzorców:</span><span class="sxs-lookup"><span data-stu-id="eef8d-160">In the **Sign On URL** textbox, type a URL using one of the following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
   
    <span data-ttu-id="eef8d-161">b.</span><span class="sxs-lookup"><span data-stu-id="eef8d-161">b.</span></span> <span data-ttu-id="eef8d-162">W **adres URL odpowiedzi** tekstowym, wpisz adres URL przy użyciu jednej z następujących wzorców:</span><span class="sxs-lookup"><span data-stu-id="eef8d-162">In the **Reply URL** textbox, type a URL using one of the following patterns:</span></span> 
   
    |  |
    | --- |
    | `https://<company name>.successfactors.com/<company name>` |
    | `https://<company name>.sapsf.com/<company name>` |
    | `https://<company name>.successfactors.eu/<company name>` |
    | `https://<company name>.sapsf.eu` |
    | `https://<company name>.sapsf.eu/<company name>` |
   
    <span data-ttu-id="eef8d-163">c.</span><span class="sxs-lookup"><span data-stu-id="eef8d-163">c.</span></span> <span data-ttu-id="eef8d-164">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-164">Click **Next**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="eef8d-165">Należy pamiętać, że nie są one rzeczywiste wartości.</span><span class="sxs-lookup"><span data-stu-id="eef8d-165">Please note that these are not the real values.</span></span> <span data-ttu-id="eef8d-166">Należy zaktualizować te wartości rzeczywistych na adres URL logowania i adres URL odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="eef8d-166">You have to update these values with the actual Sign On URL and Reply URL.</span></span> <span data-ttu-id="eef8d-167">Aby uzyskać te wartości, skontaktuj się z [SuccessFactors obsługuje zespołu](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="eef8d-167">To get these values, contact [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

1. <span data-ttu-id="eef8d-168">Na **skonfigurować logowanie jednokrotne w SuccessFactors** kliknij przycisk **pobierania certyfikatu**, a następnie zapisz plik certyfikatu lokalnie na komputerze.</span><span class="sxs-lookup"><span data-stu-id="eef8d-168">On the **Configure single sign-on at SuccessFactors** page, click **Download certificate**, and then save the certificate file locally on your computer.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][10]

2. <span data-ttu-id="eef8d-170">W oknie przeglądarki innej witryny sieci web, zaloguj się do Twojego **portalu administracyjnego SuccessFactors** jako administrator.</span><span class="sxs-lookup"><span data-stu-id="eef8d-170">In a different web browser window, log into your **SuccessFactors admin portal** as an administrator.</span></span>

3. <span data-ttu-id="eef8d-171">Odwiedź stronę **zabezpieczeń aplikacji** i macierzysty **pojedynczy znak w funkcji**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-171">Visit **Application Security** and native to **Single Sign On Feature**.</span></span> 

4. <span data-ttu-id="eef8d-172">Umieść wszystkie wartości w **zresetować tokenu** i kliknij przycisk **zapisać tokenu** do włączenia funkcji logowania jednokrotnego SAML.</span><span class="sxs-lookup"><span data-stu-id="eef8d-172">Place any value in the **Reset Token** and click **Save Token** to enable SAML SSO.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji][11]

    > [!NOTE] 
    > <span data-ttu-id="eef8d-174">Ta wartość jest używana tylko jako przełącznika wł. / wył.</span><span class="sxs-lookup"><span data-stu-id="eef8d-174">This value is just used as the on/off switch.</span></span> <span data-ttu-id="eef8d-175">Po zapisaniu wartości logowania jednokrotnego SAML jest włączone.</span><span class="sxs-lookup"><span data-stu-id="eef8d-175">If any value is saved, the SAML SSO is ON.</span></span> <span data-ttu-id="eef8d-176">Po zapisaniu pustego logowania jednokrotnego SAML jest wyłączona.</span><span class="sxs-lookup"><span data-stu-id="eef8d-176">If a blank value is saved the SAML SSO is OFF.</span></span>

1. <span data-ttu-id="eef8d-177">Macierzysty poniżej zrzut ekranu i wykonaj następujące czynności.</span><span class="sxs-lookup"><span data-stu-id="eef8d-177">Native to below screenshot and perform the following actions.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji][12]
   
    <span data-ttu-id="eef8d-179">a.</span><span class="sxs-lookup"><span data-stu-id="eef8d-179">a.</span></span> <span data-ttu-id="eef8d-180">Wybierz **logowania jednokrotnego SAML v2** przycisk radiowy</span><span class="sxs-lookup"><span data-stu-id="eef8d-180">Select the **SAML v2 SSO** Radio Button</span></span>
   
    <span data-ttu-id="eef8d-181">b.</span><span class="sxs-lookup"><span data-stu-id="eef8d-181">b.</span></span> <span data-ttu-id="eef8d-182">Ustaw Name(e.g. SAml issuer + company name) strona zostanie SAML.</span><span class="sxs-lookup"><span data-stu-id="eef8d-182">Set the SAML Asserting Party Name(e.g. SAml issuer + company name).</span></span>
   
    <span data-ttu-id="eef8d-183">c.</span><span class="sxs-lookup"><span data-stu-id="eef8d-183">c.</span></span> <span data-ttu-id="eef8d-184">W **wystawcy SAML** pole tekstowe umieścić wartość elementu **adres URL wystawcy** z Kreatora konfiguracji aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eef8d-184">In the **SAML Issuer** textbox put the value of **Issuer URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="eef8d-185">d.</span><span class="sxs-lookup"><span data-stu-id="eef8d-185">d.</span></span> <span data-ttu-id="eef8d-186">Wybierz **odpowiedzi (odbiorcy wygenerowanych/IdP/AP)** jako **wymagają podpisu obowiązkowe**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-186">Select **Response(Customer Generated/IdP/AP)** as **Require Mandatory Signature**.</span></span>
   
    <span data-ttu-id="eef8d-187">e.</span><span class="sxs-lookup"><span data-stu-id="eef8d-187">e.</span></span> <span data-ttu-id="eef8d-188">Wybierz **włączone** jako **Włącz flagę SAML**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-188">Select **Enabled** as **Enable SAML Flag**.</span></span>
   
    <span data-ttu-id="eef8d-189">f.</span><span class="sxs-lookup"><span data-stu-id="eef8d-189">f.</span></span> <span data-ttu-id="eef8d-190">Wybierz **nr** jako **podpisu żądania logowania (rz wygenerowanych/SP/RP)**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-190">Select **No** as **Login Request Signature(SF Generated/SP/RP)**.</span></span>
   
    <span data-ttu-id="eef8d-191">g.</span><span class="sxs-lookup"><span data-stu-id="eef8d-191">g.</span></span> <span data-ttu-id="eef8d-192">Wybierz **profilu przeglądarki lub używanego po** jako **profilu SAML**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-192">Select **Browser/Post Profile** as **SAML Profile**.</span></span>
   
    <span data-ttu-id="eef8d-193">h.</span><span class="sxs-lookup"><span data-stu-id="eef8d-193">h.</span></span> <span data-ttu-id="eef8d-194">Wybierz **nr** jako **wymusić nieprawidłowy okres certyfikatu**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-194">Select **No** as **Enforce Certificate Valid Period**.</span></span>
   
    <span data-ttu-id="eef8d-195">i.</span><span class="sxs-lookup"><span data-stu-id="eef8d-195">i.</span></span> <span data-ttu-id="eef8d-196">Skopiuj zawartość pliku pobranego certyfikatu, a następnie wklej go do **certyfikatu weryfikacji SAML** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="eef8d-196">Copy the content of the downloaded certificate file, and then paste it into the **SAML Verifying Certificate** textbox.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="eef8d-197">Zawartość certyfikatu musi mieć rozpocząć certyfikatu i na końcu tagi certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="eef8d-197">The certificate content must have begin certificate and end certificate tags.</span></span>

1. <span data-ttu-id="eef8d-198">Przejdź do SAML V2, a następnie wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="eef8d-198">Navigate to SAML V2, and then perform the following steps:</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej po stronie aplikacji][13]
   
    <span data-ttu-id="eef8d-200">a.</span><span class="sxs-lookup"><span data-stu-id="eef8d-200">a.</span></span> <span data-ttu-id="eef8d-201">Wybierz **tak** jako **inicjowane SP wylogowania globalnego obsługują**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-201">Select **Yes** as **Support SP-initiated Global Logout**.</span></span>
   
    <span data-ttu-id="eef8d-202">b.</span><span class="sxs-lookup"><span data-stu-id="eef8d-202">b.</span></span> <span data-ttu-id="eef8d-203">W **globalne wylogowania adres URL usługi (LogoutRequest docelowy)** pole tekstowe umieścić wartość elementu **zdalnego adresu URL wylogowania** z Kreatora konfiguracji aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eef8d-203">In the **Global Logout Service URL (LogoutRequest destination)** textbox put the value of **Remote Logout URL** from Azure AD application configuration wizard.</span></span>
   
    <span data-ttu-id="eef8d-204">c.</span><span class="sxs-lookup"><span data-stu-id="eef8d-204">c.</span></span> <span data-ttu-id="eef8d-205">Wybierz **nr** jako **wymagają sp należy szyfrować wszystkie element NameID**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-205">Select **No** as **Require sp must encrypt all NameID element**.</span></span>
   
    <span data-ttu-id="eef8d-206">d.</span><span class="sxs-lookup"><span data-stu-id="eef8d-206">d.</span></span> <span data-ttu-id="eef8d-207">Wybierz **nieokreślony** jako **NameID Format**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-207">Select **unspecified** as **NameID Format**.</span></span>
   
    <span data-ttu-id="eef8d-208">e.</span><span class="sxs-lookup"><span data-stu-id="eef8d-208">e.</span></span> <span data-ttu-id="eef8d-209">Wybierz **tak** jako **Włącz sp zainicjował logowania (AuthnRequest)**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-209">Select **Yes** as **Enable sp initiated login (AuthnRequest)**.</span></span>
   
    <span data-ttu-id="eef8d-210">f.</span><span class="sxs-lookup"><span data-stu-id="eef8d-210">f.</span></span> <span data-ttu-id="eef8d-211">W **żądanie wysłania jako wystawca firmie** pole tekstowe umieścić wartość elementu **zdalnego adresu URL logowania** z Kreatora konfiguracji aplikacji usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="eef8d-211">In the **Send request as Company-Wide issuer** textbox put the value of **Remote Login URL** from Azure AD application configuration wizard.</span></span>
2. <span data-ttu-id="eef8d-212">Wykonaj następujące kroki, aby wprowadzić nazwy logowania użytkowników bez uwzględniania wielkości liter,.</span><span class="sxs-lookup"><span data-stu-id="eef8d-212">Perform these steps if you want to make the login usernames Case Insensitive, .</span></span>
   
    <span data-ttu-id="eef8d-213">a.</span><span class="sxs-lookup"><span data-stu-id="eef8d-213">a.</span></span> <span data-ttu-id="eef8d-214">Odwiedź stronę **ustawienia firmy**(w dolnej).</span><span class="sxs-lookup"><span data-stu-id="eef8d-214">Visit **Company Settings**(near the bottom).</span></span>
   
    <span data-ttu-id="eef8d-215">b.</span><span class="sxs-lookup"><span data-stu-id="eef8d-215">b.</span></span> <span data-ttu-id="eef8d-216">Zaznacz pole wyboru obok **włączyć Username Non-uwzględniana wielkość liter**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-216">select checkbox near **Enable Non-Case-Sensitive Username**.</span></span>
   
    <span data-ttu-id="eef8d-217">c.Click **zapisać**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-217">c.Click **Save**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][29]

    > [!NOTE] 
    > <span data-ttu-id="eef8d-219">Jeśli spróbujesz je włączyć, system sprawdza, czy spowoduje utworzenie zduplikowanej nazwy logowania SAML.</span><span class="sxs-lookup"><span data-stu-id="eef8d-219">If you try to enable this, the system checks if it will create a duplicate SAML login name.</span></span> <span data-ttu-id="eef8d-220">Na przykład, jeśli klient ma nazw użytkowników Użytkownik1 i Użytkownik1.</span><span class="sxs-lookup"><span data-stu-id="eef8d-220">For example if the customer has usernames User1 and user1.</span></span> <span data-ttu-id="eef8d-221">Zdjęciu uwzględniana wielkość liter powoduje, że te duplikaty.</span><span class="sxs-lookup"><span data-stu-id="eef8d-221">Taking away case sensitivity makes these duplicates.</span></span> <span data-ttu-id="eef8d-222">System otrzymasz komunikat o błędzie i nie włączy tę funkcję.</span><span class="sxs-lookup"><span data-stu-id="eef8d-222">The system will give you an error message and will not enable the feature.</span></span> <span data-ttu-id="eef8d-223">Klienta należy zmienić jedną z nazw użytkowników, tak faktycznie Pisownia jest inny.</span><span class="sxs-lookup"><span data-stu-id="eef8d-223">The customer will need to change one of the usernames so it’s actually spelled different.</span></span> 

1. <span data-ttu-id="eef8d-224">W klasycznym portalu Azure, wybierz Potwierdzenie konfiguracji rejestracji jednokrotnej, a następnie kliknij przycisk **Complete** zamknąć **skonfigurować rejestrację jednokrotną** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eef8d-224">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
   
    ![Aplikacje][14]
2. <span data-ttu-id="eef8d-226">Na **pojedynczy znak na potwierdzenie** kliknij przycisk **Complete**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-226">On the **Single sign-on confirmation** page, click **Complete**.</span></span>
   
    ![Aplikacje][15]

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="eef8d-228">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="eef8d-228">Creating an Azure AD test user</span></span>
<span data-ttu-id="eef8d-229">Celem tej sekcji jest tworzenie użytkownika testowego w klasycznym portalu o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="eef8d-229">The objective of this section is to create a test user in the classic portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][16]

<span data-ttu-id="eef8d-231">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="eef8d-231">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="eef8d-232">W **klasycznego portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-232">In the **Azure classic Portal**, on the left navigation pane, click **Active Directory**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][17]
2. <span data-ttu-id="eef8d-234">Z **katalogu** listy, wybierz katalog, dla którego chcesz włączyć integracji katalogów.</span><span class="sxs-lookup"><span data-stu-id="eef8d-234">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="eef8d-235">Aby wyświetlić listę użytkowników, w menu u góry, kliknij przycisk **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-235">To display the list of users, in the menu on the top, click **Users**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][18]
4. <span data-ttu-id="eef8d-237">Aby otworzyć **Dodaj użytkownika** okna dialogowego na pasku narzędzi u dołu, kliknij przycisk **Dodaj użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-237">To open the **Add User** dialog, in the toolbar on the bottom, click **Add User**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][19]
5. <span data-ttu-id="eef8d-239">Na **Poinformuj nas o tym użytkowniku** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="eef8d-239">On the **Tell us about this user** dialog page, perform the following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][20]
   
    <span data-ttu-id="eef8d-241">a.</span><span class="sxs-lookup"><span data-stu-id="eef8d-241">a.</span></span> <span data-ttu-id="eef8d-242">Jako typ użytkownika wybierz nowego użytkownika w organizacji.</span><span class="sxs-lookup"><span data-stu-id="eef8d-242">As Type Of User, select New user in your organization.</span></span>
   
    <span data-ttu-id="eef8d-243">b.</span><span class="sxs-lookup"><span data-stu-id="eef8d-243">b.</span></span> <span data-ttu-id="eef8d-244">W nazwie użytkownika **pole tekstowe**, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-244">In the User Name **textbox**, type **BrittaSimon**.</span></span>
   
    <span data-ttu-id="eef8d-245">c.</span><span class="sxs-lookup"><span data-stu-id="eef8d-245">c.</span></span> <span data-ttu-id="eef8d-246">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-246">Click **Next**.</span></span>
6. <span data-ttu-id="eef8d-247">Na **profilu użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="eef8d-247">On the **User Profile** dialog page, perform the following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][21]
   
    <span data-ttu-id="eef8d-249">a.</span><span class="sxs-lookup"><span data-stu-id="eef8d-249">a.</span></span> <span data-ttu-id="eef8d-250">W **imię** pole tekstowe, typ **Britta**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-250">In the **First Name** textbox, type **Britta**.</span></span>  
   
    <span data-ttu-id="eef8d-251">b.</span><span class="sxs-lookup"><span data-stu-id="eef8d-251">b.</span></span> <span data-ttu-id="eef8d-252">W **nazwisko** pole tekstowe, typ **Simona**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-252">In the **Last Name** textbox, type, **Simon**.</span></span>
   
    <span data-ttu-id="eef8d-253">c.</span><span class="sxs-lookup"><span data-stu-id="eef8d-253">c.</span></span> <span data-ttu-id="eef8d-254">W **Nazwa wyświetlana** pole tekstowe, typ **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-254">In the **Display Name** textbox, type **Britta Simon**.</span></span>
   
    <span data-ttu-id="eef8d-255">d.</span><span class="sxs-lookup"><span data-stu-id="eef8d-255">d.</span></span> <span data-ttu-id="eef8d-256">W **roli** listy, wybierz **użytkownika**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-256">In the **Role** list, select **User**.</span></span>
   
    <span data-ttu-id="eef8d-257">e.</span><span class="sxs-lookup"><span data-stu-id="eef8d-257">e.</span></span> <span data-ttu-id="eef8d-258">Kliknij przycisk **Dalej**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-258">Click **Next**.</span></span>
7. <span data-ttu-id="eef8d-259">Na **Uzyskaj hasło tymczasowe** strony okna dialogowego, kliknij przycisk **utworzyć**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-259">On the **Get temporary password** dialog page, click **create**.</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][22]
8. <span data-ttu-id="eef8d-261">Na **Uzyskaj hasło tymczasowe** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="eef8d-261">On the **Get temporary password** dialog page, perform the following steps:</span></span>
   
    ![Tworzenie użytkownika testowego usługi Azure AD][23]
   
    <span data-ttu-id="eef8d-263">a.</span><span class="sxs-lookup"><span data-stu-id="eef8d-263">a.</span></span> <span data-ttu-id="eef8d-264">Zanotuj wartość **nowe hasło**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-264">Write down the value of the **New Password**.</span></span>
   
    <span data-ttu-id="eef8d-265">b.</span><span class="sxs-lookup"><span data-stu-id="eef8d-265">b.</span></span> <span data-ttu-id="eef8d-266">Kliknij przycisk **Complete** (Zakończ).</span><span class="sxs-lookup"><span data-stu-id="eef8d-266">Click **Complete**.</span></span>  

### <a name="creating-a-successfactors-test-user"></a><span data-ttu-id="eef8d-267">Tworzenie użytkownika testowego SuccessFactors</span><span class="sxs-lookup"><span data-stu-id="eef8d-267">Creating a SuccessFactors test user</span></span>
<span data-ttu-id="eef8d-268">Aby włączyć użytkowników usługi Azure AD zalogować się do SuccessFactors, musi być przygotowana do SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="eef8d-268">In order to enable Azure AD users to log into SuccessFactors, they must be provisioned into SuccessFactors.</span></span>  
<span data-ttu-id="eef8d-269">W przypadku SuccessFactors Inicjowanie obsługi to zadanie ręczne.</span><span class="sxs-lookup"><span data-stu-id="eef8d-269">In the case of SuccessFactors, provisioning is a manual task.</span></span>

<span data-ttu-id="eef8d-270">Aby uzyskać użytkownicy utworzeni w SuccessFactors, należy skontaktować się [SuccessFactors obsługuje zespołu](https://www.successfactors.com/en_us/support.html).</span><span class="sxs-lookup"><span data-stu-id="eef8d-270">To get users created in SuccessFactors, you need to contact the [SuccessFactors support team](https://www.successfactors.com/en_us/support.html).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="eef8d-271">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="eef8d-271">Assigning the Azure AD test user</span></span>
<span data-ttu-id="eef8d-272">Celem tej sekcji jest włączenie Simona Britta do udostępnienia jej SuccessFactors za pomocą usługi Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="eef8d-272">The objective of this section is to enabling Britta Simon to use Azure single sign-on by granting her access to SuccessFactors.</span></span>

![Przypisz użytkownika][24]

<span data-ttu-id="eef8d-274">**Aby przypisać Simona Britta SuccessFactors, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="eef8d-274">**To assign Britta Simon to SuccessFactors, perform the following steps:**</span></span>

1. <span data-ttu-id="eef8d-275">W klasycznym portalu, aby otworzyć widok aplikacji, w widoku katalogu, kliknij przycisk **aplikacji** w menu u góry.</span><span class="sxs-lookup"><span data-stu-id="eef8d-275">On the classic portal, to open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
    ![Przypisz użytkownika][25]
2. <span data-ttu-id="eef8d-277">Na liście aplikacji zaznacz **SuccessFactors**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-277">In the applications list, select **SuccessFactors**.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej][26]
3. <span data-ttu-id="eef8d-279">W menu u góry kliknij **użytkowników**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-279">In the menu on the top, click **Users**.</span></span>
   
    ![Przypisz użytkownika][27]
4. <span data-ttu-id="eef8d-281">Na liście użytkowników wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-281">In the Users list, select **Britta Simon**.</span></span>
5. <span data-ttu-id="eef8d-282">Na pasku narzędzi u dołu, kliknij przycisk **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="eef8d-282">In the toolbar on the bottom, click **Assign**.</span></span>
   
    ![Przypisz użytkownika][28]

### <a name="testing-single-sign-on"></a><span data-ttu-id="eef8d-284">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="eef8d-284">Testing single sign-on</span></span>
<span data-ttu-id="eef8d-285">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="eef8d-285">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="eef8d-286">Po kliknięciu kafelka SuccessFactors w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji SuccessFactors.</span><span class="sxs-lookup"><span data-stu-id="eef8d-286">When you click the SuccessFactors tile in the Access Panel, you should get automatically signed-on to your SuccessFactors application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eef8d-287">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="eef8d-287">Additional resources</span></span>
* [<span data-ttu-id="eef8d-288">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="eef8d-288">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="eef8d-289">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="eef8d-289">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[0]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_00.png
[1]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_04.png
[5]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_01.png
[6]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_02.png
[7]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_03.png
[8]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_04.png
[9]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_05.png
[10]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_06.png

[11]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_07.png
[12]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_08.png
[13]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_09.png
[14]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_05.png
[15]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_06.png

[16]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_00.png
[17]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_01.png
[18]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_02.png
[19]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_03.png
[20]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_04.png
[21]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_05.png
[22]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_06.png
[23]: ./media/active-directory-saas-successfactors-tutorial/create_aaduser_07.png

[24]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_07.png
[25]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_08.png
[26]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_11.png
[27]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_09.png
[28]: ./media/active-directory-saas-successfactors-tutorial/tutorial_general_10.png
[29]: ./media/active-directory-saas-successfactors-tutorial/tutorial_successfactors_10.png
