---
title: "Samouczek: Integracji Azure Active Directory z chmurą SAP dla klienta | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować logowanie jednokrotne między usługą Azure Active Directory i w chmurze SAP dla klienta."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: e4d945525a45704f34e1d9e742220928a516f341
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a><span data-ttu-id="81be3-103">Samouczek: Integracji Azure Active Directory z chmurą SAP dla klienta</span><span class="sxs-lookup"><span data-stu-id="81be3-103">Tutorial: Azure Active Directory integration with SAP Cloud for Customer</span></span>

<span data-ttu-id="81be3-104">Z tego samouczka dowiesz się integrowanie SAP chmury dla klienta w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="81be3-104">In this tutorial, you learn how to integrate SAP Cloud for Customer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="81be3-105">Integrowanie SAP chmury dla klienta z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="81be3-105">Integrating SAP Cloud for Customer with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="81be3-106">Można kontrolować w usłudze Azure AD, który ma dostęp do chmury SAP dla klienta</span><span class="sxs-lookup"><span data-stu-id="81be3-106">You can control in Azure AD who has access to SAP Cloud for Customer</span></span>
- <span data-ttu-id="81be3-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do chmury SAP dla klienta (logowanie jednokrotne) przy użyciu ich kont usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="81be3-107">You can enable your users to automatically get signed-on to SAP Cloud for Customer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="81be3-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="81be3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="81be3-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="81be3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81be3-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="81be3-110">Prerequisites</span></span>

<span data-ttu-id="81be3-111">Aby skonfigurować integrację usługi Azure AD z chmurą SAP dla odbiorcy, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="81be3-111">To configure Azure AD integration with SAP Cloud for Customer, you need the following items:</span></span>

- <span data-ttu-id="81be3-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="81be3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="81be3-113">Chmurę SAP do klienta logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="81be3-113">A SAP Cloud for Customer single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="81be3-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="81be3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="81be3-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="81be3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="81be3-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="81be3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="81be3-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz pobrać miesięczna wersja próbna tutaj: [oferta wersji próbnej](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="81be3-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="81be3-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="81be3-118">Scenario description</span></span>
<span data-ttu-id="81be3-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="81be3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="81be3-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="81be3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="81be3-121">Dodawanie SAP chmury dla klienta z galerii</span><span class="sxs-lookup"><span data-stu-id="81be3-121">Adding SAP Cloud for Customer from the gallery</span></span>
2. <span data-ttu-id="81be3-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="81be3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-cloud-for-customer-from-the-gallery"></a><span data-ttu-id="81be3-123">Dodawanie SAP chmury dla klienta z galerii</span><span class="sxs-lookup"><span data-stu-id="81be3-123">Adding SAP Cloud for Customer from the gallery</span></span>
<span data-ttu-id="81be3-124">Aby skonfigurować integrację SAP chmury dla klienta do usługi Azure AD, należy dodać SAP chmury dla klienta z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="81be3-124">To configure the integration of SAP Cloud for Customer into Azure AD, you need to add SAP Cloud for Customer from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="81be3-125">**Aby dodać SAP chmury dla klienta z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="81be3-125">**To add SAP Cloud for Customer from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="81be3-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="81be3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="81be3-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="81be3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="81be3-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="81be3-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="81be3-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="81be3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="81be3-133">W polu wyszukiwania wpisz **SAP chmury dla klienta**.</span><span class="sxs-lookup"><span data-stu-id="81be3-133">In the search box, type **SAP Cloud for Customer**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. <span data-ttu-id="81be3-135">W panelu wyników wybierz **SAP chmury dla klienta**, a następnie kliknij przycisk **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="81be3-135">In the results panel, select **SAP Cloud for Customer**, and then click **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="81be3-137">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="81be3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="81be3-138">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z chmurą SAP dla klienta w oparciu o użytkownika testowego o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="81be3-138">In this section, you configure and test Azure AD single sign-on with SAP Cloud for Customer based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="81be3-139">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w chmurze SAP dla klienta jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="81be3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Cloud for Customer is to a user in Azure AD.</span></span> <span data-ttu-id="81be3-140">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w chmurze SAP dla klienta.</span><span class="sxs-lookup"><span data-stu-id="81be3-140">In other words, a link relationship between an Azure AD user and the related user in SAP Cloud for Customer needs to be established.</span></span>

<span data-ttu-id="81be3-141">W chmurze SAP dla klienta, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="81be3-141">In SAP Cloud for Customer, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="81be3-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z chmurą SAP dla klienta, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="81be3-142">To configure and test Azure AD single sign-on with SAP Cloud for Customer, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="81be3-143">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="81be3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="81be3-144">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="81be3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="81be3-145">**[Tworzenie chmury SAP dla użytkownika testowego klienta](#creating-a-sap-cloud-for-customer-test-user)**  — aby odpowiednikiem Simona Britta w chmurze SAP dla klienta, który jest połączony z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="81be3-145">**[Creating a SAP Cloud for Customer test user](#creating-a-sap-cloud-for-customer-test-user)** - to have a counterpart of Britta Simon in SAP Cloud for Customer that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="81be3-146">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="81be3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="81be3-147">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="81be3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="81be3-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="81be3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="81be3-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne w chmurze SAP dla aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="81be3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Cloud for Customer application.</span></span>

<span data-ttu-id="81be3-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z chmurą SAP dla klienta, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="81be3-150">**To configure Azure AD single sign-on with SAP Cloud for Customer, perform the following steps:**</span></span>

1. <span data-ttu-id="81be3-151">W portalu Azure na **SAP chmury dla klienta** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="81be3-151">In the Azure portal, on the **SAP Cloud for Customer** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="81be3-153">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="81be3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. <span data-ttu-id="81be3-155">Na **chmury SAP do domeny klienta i adresy URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="81be3-155">On the **SAP Cloud for Customer Domain and URLs** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    <span data-ttu-id="81be3-157">a.</span><span class="sxs-lookup"><span data-stu-id="81be3-157">a.</span></span> <span data-ttu-id="81be3-158">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="81be3-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    <span data-ttu-id="81be3-159">b.</span><span class="sxs-lookup"><span data-stu-id="81be3-159">b.</span></span> <span data-ttu-id="81be3-160">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="81be3-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="81be3-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="81be3-161">These values are not real.</span></span> <span data-ttu-id="81be3-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="81be3-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="81be3-163">Skontaktuj się z [chmurę SAP do zespołu pomocy technicznej klienta klienta](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="81be3-163">Contact [SAP Cloud for Customer Client support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) to get these values.</span></span> 

4. <span data-ttu-id="81be3-164">Na **atrybuty użytkownika** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="81be3-164">On the **User Attributes** section, perform the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    <span data-ttu-id="81be3-166">a.</span><span class="sxs-lookup"><span data-stu-id="81be3-166">a.</span></span> <span data-ttu-id="81be3-167">W **identyfikator użytkownika** listy, wybierz **ExtractMailPrefix()** funkcji.</span><span class="sxs-lookup"><span data-stu-id="81be3-167">In **User Identifier** list, select the **ExtractMailPrefix()** function.</span></span>

    <span data-ttu-id="81be3-168">b.</span><span class="sxs-lookup"><span data-stu-id="81be3-168">b.</span></span> <span data-ttu-id="81be3-169">Z **poczty** wybierz atrybut użytkownika, którego chcesz użyć implementacji.</span><span class="sxs-lookup"><span data-stu-id="81be3-169">From the **Mail** list, select the user attribute you want to use for your implementation.</span></span>
    <span data-ttu-id="81be3-170">Na przykład jeśli ma być używany jako identyfikator użytkownika unikatowy identyfikator pracownika, a wartość atrybutu są przechowywane w ExtensionAttribute2, wybierz user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="81be3-170">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span></span>  

5. <span data-ttu-id="81be3-171">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="81be3-171">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. <span data-ttu-id="81be3-173">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="81be3-173">Click **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="81be3-175">Na **SAP chmury dla konfiguracji klienta** , kliknij przycisk **skonfigurować chmurę SAP do klienta** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="81be3-175">On the **SAP Cloud for Customer Configuration** section, click **Configure SAP Cloud for Customer** to open **Configure sign-on** window.</span></span> <span data-ttu-id="81be3-176">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="81be3-176">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. <span data-ttu-id="81be3-178">Aby uzyskać dostęp skonfigurowane logowania jednokrotnego, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="81be3-178">To get SSO configured, perform the following steps:</span></span>
   
    <span data-ttu-id="81be3-179">a.</span><span class="sxs-lookup"><span data-stu-id="81be3-179">a.</span></span> <span data-ttu-id="81be3-180">Zaloguj się w chmurze SAP do portalu klienta z prawami administratora.</span><span class="sxs-lookup"><span data-stu-id="81be3-180">Login into SAP Cloud for Customer portal with administrator rights.</span></span>
   
    <span data-ttu-id="81be3-181">b.</span><span class="sxs-lookup"><span data-stu-id="81be3-181">b.</span></span> <span data-ttu-id="81be3-182">Przejdź do **aplikacji i typowych zadań zarządzania użytkownika** i kliknij przycisk **dostawcy tożsamości** kartę.</span><span class="sxs-lookup"><span data-stu-id="81be3-182">Navigate to the **Application and User Management Common Task** and click the **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="81be3-183">c.</span><span class="sxs-lookup"><span data-stu-id="81be3-183">c.</span></span> <span data-ttu-id="81be3-184">Kliknij przycisk **nowego dostawcy tożsamości** i wybierz plik XML metadanych został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="81be3-184">Click **New Identity Provider** and select the metadata XML file you have downloaded from the Azure portal.</span></span> <span data-ttu-id="81be3-185">Przez importowanie metadanych, system automatycznie wysyła certyfikat wymagany podpis, jak i certyfikat szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="81be3-185">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    <span data-ttu-id="81be3-187">d.</span><span class="sxs-lookup"><span data-stu-id="81be3-187">d.</span></span> <span data-ttu-id="81be3-188">Usługa Azure Active Directory wymaga elementu adres URL usługi klienta potwierdzenia w żądaniu SAML, dlatego wybierz **zawierają potwierdzenie konsumenta adres URL usługi** wyboru.</span><span class="sxs-lookup"><span data-stu-id="81be3-188">Azure Active Directory requires the element Assertion Consumer Service URL in the SAML request, so select the **Include Assertion Consumer Service URL** checkbox.</span></span>
   
    <span data-ttu-id="81be3-189">e.</span><span class="sxs-lookup"><span data-stu-id="81be3-189">e.</span></span> <span data-ttu-id="81be3-190">Kliknij przycisk **aktywacji rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="81be3-190">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="81be3-191">f.</span><span class="sxs-lookup"><span data-stu-id="81be3-191">f.</span></span> <span data-ttu-id="81be3-192">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="81be3-192">Save your changes.</span></span>
   
    <span data-ttu-id="81be3-193">g.</span><span class="sxs-lookup"><span data-stu-id="81be3-193">g.</span></span> <span data-ttu-id="81be3-194">Kliknij przycisk **systemie** kartę.</span><span class="sxs-lookup"><span data-stu-id="81be3-194">Click the **My System** tab.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    <span data-ttu-id="81be3-196">h.</span><span class="sxs-lookup"><span data-stu-id="81be3-196">h.</span></span> <span data-ttu-id="81be3-197">W **Azure AD znaku w adresie URL** pole tekstowe, Wklej **SAML pojedynczy znak na adres URL usługi** którego została skopiowana z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="81be3-197">In **Azure AD Sign On URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    <span data-ttu-id="81be3-199">i.</span><span class="sxs-lookup"><span data-stu-id="81be3-199">i.</span></span> <span data-ttu-id="81be3-200">Określ, czy pracownik może ręcznie wybrać między zalogowanie się przy użyciu Identyfikatora użytkownika i hasła lub logowania jednokrotnego, wybierając **wybór dostawcy tożsamości ręcznego**.</span><span class="sxs-lookup"><span data-stu-id="81be3-200">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting the **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="81be3-201">j.</span><span class="sxs-lookup"><span data-stu-id="81be3-201">j.</span></span> <span data-ttu-id="81be3-202">W **adres URL logowania jednokrotnego** sekcji, podaj adres URL, które mają być używane przez pracowników do logowania do systemu.</span><span class="sxs-lookup"><span data-stu-id="81be3-202">In the **SSO URL** section, specify the URL that should be used by your employees to sign on to the system.</span></span> 
    <span data-ttu-id="81be3-203">W **adres URL wysyłane do pracowników** liście, można wybrać jedną z następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="81be3-203">In the **URL Sent to Employee** list, you can choose between the following options:</span></span>
   
    <span data-ttu-id="81be3-204">**Adres URL — Usługa rejestracji Jednokrotnej**</span><span class="sxs-lookup"><span data-stu-id="81be3-204">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="81be3-205">System wysyła tylko adres URL normalne systemu do pracownika.</span><span class="sxs-lookup"><span data-stu-id="81be3-205">The system sends only the normal system URL to the employee.</span></span> <span data-ttu-id="81be3-206">Pracownik nie może zalogować się przy użyciu logowania jednokrotnego i musi użyć hasła lub zamiast tego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="81be3-206">The employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="81be3-207">**ADRES URL LOGOWANIA JEDNOKROTNEGO**</span><span class="sxs-lookup"><span data-stu-id="81be3-207">**SSO URL**</span></span> 
   
    <span data-ttu-id="81be3-208">System wysyła tylko adres URL logowania jednokrotnego do pracownika.</span><span class="sxs-lookup"><span data-stu-id="81be3-208">The system sends only the SSO URL to the employee.</span></span> <span data-ttu-id="81be3-209">Pracownik może zalogować się przy użyciu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="81be3-209">The employee can log on using SSO.</span></span> <span data-ttu-id="81be3-210">Żądanie uwierzytelnienia jest przekierowywane przez dostawców tożsamości.</span><span class="sxs-lookup"><span data-stu-id="81be3-210">Authentication request is redirected through the IdP.</span></span>
   
    <span data-ttu-id="81be3-211">**Automatyczne wybieranie**</span><span class="sxs-lookup"><span data-stu-id="81be3-211">**Automatic Selection**</span></span>
   
    <span data-ttu-id="81be3-212">Jeśli logowania jednokrotnego nie jest aktywne, system wysyła system normalny adres URL do pracownika.</span><span class="sxs-lookup"><span data-stu-id="81be3-212">If SSO is not active, the system sends the normal system URL to the employee.</span></span> <span data-ttu-id="81be3-213">Jeśli usługa rejestracji Jednokrotnej jest aktywny, system sprawdza, czy pracownik ma hasło.</span><span class="sxs-lookup"><span data-stu-id="81be3-213">If SSO is active, the system checks whether the employee has a password.</span></span> <span data-ttu-id="81be3-214">Jeśli hasło jest dostępny, zarówno adres URL logowania jednokrotnego i adres URL logowania jednokrotnego nie są wysyłane do pracownika.</span><span class="sxs-lookup"><span data-stu-id="81be3-214">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span></span> <span data-ttu-id="81be3-215">Jeśli pracownik nie ma hasła, adres URL logowania jednokrotnego są wysyłane do pracownika.</span><span class="sxs-lookup"><span data-stu-id="81be3-215">However, if the employee has no password, only the SSO URL is sent to the employee.</span></span>
   
    <span data-ttu-id="81be3-216">k.</span><span class="sxs-lookup"><span data-stu-id="81be3-216">k.</span></span> <span data-ttu-id="81be3-217">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="81be3-217">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="81be3-218">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="81be3-218">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="81be3-219">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="81be3-219">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="81be3-220">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="81be3-220">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="81be3-221">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="81be3-221">Creating an Azure AD test user</span></span>
<span data-ttu-id="81be3-222">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="81be3-222">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="81be3-224">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="81be3-224">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="81be3-225">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="81be3-225">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="81be3-227">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="81be3-227">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="81be3-229">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="81be3-229">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="81be3-231">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="81be3-231">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="81be3-233">a.</span><span class="sxs-lookup"><span data-stu-id="81be3-233">a.</span></span> <span data-ttu-id="81be3-234">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="81be3-234">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="81be3-235">b.</span><span class="sxs-lookup"><span data-stu-id="81be3-235">b.</span></span> <span data-ttu-id="81be3-236">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="81be3-236">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="81be3-237">c.</span><span class="sxs-lookup"><span data-stu-id="81be3-237">c.</span></span> <span data-ttu-id="81be3-238">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="81be3-238">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="81be3-239">d.</span><span class="sxs-lookup"><span data-stu-id="81be3-239">d.</span></span> <span data-ttu-id="81be3-240">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="81be3-240">Click **Create**.</span></span>
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a><span data-ttu-id="81be3-241">Tworzenie chmury SAP dla użytkownika testowego klienta</span><span class="sxs-lookup"><span data-stu-id="81be3-241">Creating a SAP Cloud for Customer test user</span></span>

<span data-ttu-id="81be3-242">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w chmurze SAP dla klienta.</span><span class="sxs-lookup"><span data-stu-id="81be3-242">In this section, you create a user called Britta Simon in SAP Cloud for Customer.</span></span> <span data-ttu-id="81be3-243">We współpracy z [SAP chmury zespół obsługi klienta](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) Aby dodać użytkowników w chmurze SAP platformy klienta.</span><span class="sxs-lookup"><span data-stu-id="81be3-243">Please work with [SAP Cloud for Customer support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) to add the users in the SAP Cloud for Customer platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="81be3-244">Upewnij się, wartość NameID powinny być zgodne z pola Nazwa użytkownika w chmurze SAP dla klienta platformy.</span><span class="sxs-lookup"><span data-stu-id="81be3-244">Please make sure that NameID value should match with the username field in the SAP Cloud for Customer platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="81be3-245">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="81be3-245">Assigning the Azure AD test user</span></span>

<span data-ttu-id="81be3-246">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do chmury SAP dla klienta.</span><span class="sxs-lookup"><span data-stu-id="81be3-246">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Cloud for Customer.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="81be3-248">**Aby przypisać Simona Britta SAP chmury dla klienta, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="81be3-248">**To assign Britta Simon to SAP Cloud for Customer, perform the following steps:**</span></span>

1. <span data-ttu-id="81be3-249">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="81be3-249">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="81be3-251">Na liście aplikacji zaznacz **SAP chmury dla klienta**.</span><span class="sxs-lookup"><span data-stu-id="81be3-251">In the applications list, select **SAP Cloud for Customer**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. <span data-ttu-id="81be3-253">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="81be3-253">In the menu on the left, click **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="81be3-255">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="81be3-255">Click **Add** button.</span></span> <span data-ttu-id="81be3-256">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="81be3-256">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="81be3-258">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="81be3-258">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="81be3-259">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="81be3-259">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="81be3-260">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="81be3-260">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="81be3-261">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="81be3-261">Testing single sign-on</span></span>

<span data-ttu-id="81be3-262">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="81be3-262">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="81be3-263">Po kliknięciu chmury SAP do klienta kafelka w panelu dostępu należy należy pobrać automatycznie zalogowane z Twoją chmurą SAP dla aplikacji klienta.</span><span class="sxs-lookup"><span data-stu-id="81be3-263">When you click the SAP Cloud for Customer tile in the Access Panel, you should get automatically signed-on to your SAP Cloud for Customer application.</span></span>
<span data-ttu-id="81be3-264">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="81be3-264">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="81be3-265">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="81be3-265">Additional resources</span></span>

* [<span data-ttu-id="81be3-266">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="81be3-266">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="81be3-267">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="81be3-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

