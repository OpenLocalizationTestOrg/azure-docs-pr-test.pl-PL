---
title: 'Samouczek: Integracji Azure Active Directory z SAP Business ByDesign | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i SAP Business ByDesign."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 82938920-33ba-47cb-b141-511b46d19e66
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: ab76a0ac1ef954efd3c66e6f565514b889ed9444
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-business-bydesign"></a><span data-ttu-id="24a4f-103">Samouczek: integracja usługi Azure Active Directory z oprogramowaniem SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="24a4f-103">Tutorial: Azure Active Directory integration with SAP Business ByDesign</span></span>

<span data-ttu-id="24a4f-104">Z tego samouczka dowiesz się integrowanie SAP Business ByDesign z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="24a4f-104">In this tutorial, you learn how to integrate SAP Business ByDesign with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="24a4f-105">Integrowanie SAP Business ByDesign z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="24a4f-105">Integrating SAP Business ByDesign with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="24a4f-106">Można kontrolować w usłudze Azure AD, który ma dostęp do programu SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="24a4f-106">You can control in Azure AD who has access to SAP Business ByDesign.</span></span>
- <span data-ttu-id="24a4f-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do SAP Business ByDesign (logowanie jednokrotne) z konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24a4f-107">You can enable your users to automatically get signed-on to SAP Business ByDesign (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="24a4f-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="24a4f-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="24a4f-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="24a4f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24a4f-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="24a4f-110">Prerequisites</span></span>

<span data-ttu-id="24a4f-111">Aby skonfigurować integrację usługi Azure AD z SAP Business ByDesign, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="24a4f-111">To configure Azure AD integration with SAP Business ByDesign, you need the following items:</span></span>

- <span data-ttu-id="24a4f-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="24a4f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="24a4f-113">SAP Business ByDesign logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="24a4f-113">An SAP Business ByDesign single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="24a4f-114">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="24a4f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="24a4f-115">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="24a4f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="24a4f-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="24a4f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="24a4f-117">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="24a4f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="24a4f-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="24a4f-118">Scenario description</span></span>
<span data-ttu-id="24a4f-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="24a4f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="24a4f-120">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="24a4f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="24a4f-121">Dodawanie SAP Business ByDesign z galerii</span><span class="sxs-lookup"><span data-stu-id="24a4f-121">Adding SAP Business ByDesign from the gallery</span></span>
2. <span data-ttu-id="24a4f-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="24a4f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-business-bydesign-from-the-gallery"></a><span data-ttu-id="24a4f-123">Dodawanie SAP Business ByDesign z galerii</span><span class="sxs-lookup"><span data-stu-id="24a4f-123">Adding SAP Business ByDesign from the gallery</span></span>
<span data-ttu-id="24a4f-124">Aby skonfigurować integrację usługi Azure AD SAP Business ByDesign, należy dodać SAP Business ByDesign z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="24a4f-124">To configure the integration of SAP Business ByDesign into Azure AD, you need to add SAP Business ByDesign from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="24a4f-125">**Aby dodać SAP Business ByDesign z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="24a4f-125">**To add SAP Business ByDesign from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="24a4f-126">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="24a4f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="24a4f-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="24a4f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="24a4f-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="24a4f-129">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="24a4f-131">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="24a4f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="24a4f-133">W polu wyszukiwania wpisz **SAP Business ByDesign**, wybierz pozycję **SAP Business ByDesign** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="24a4f-133">In the search box, type **SAP Business ByDesign**, select **SAP Business ByDesign** from result panel then click **Add** button to add the application.</span></span>

    ![SAP Business ByDesign na liście wyników](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="24a4f-135">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="24a4f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="24a4f-136">W tej sekcji skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SAP Business ByDesign w oparciu o nazwie "Britta Simona" użytkownika testowego.</span><span class="sxs-lookup"><span data-stu-id="24a4f-136">In this section, you configure and test Azure AD single sign-on with SAP Business ByDesign based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="24a4f-137">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w SAP Business ByDesign jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="24a4f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP Business ByDesign is to a user in Azure AD.</span></span> <span data-ttu-id="24a4f-138">Innymi słowy link relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w SAP Business ByDesign musi się.</span><span class="sxs-lookup"><span data-stu-id="24a4f-138">In other words, a link relationship between an Azure AD user and the related user in SAP Business ByDesign needs to be established.</span></span>

<span data-ttu-id="24a4f-139">W SAP Business ByDesign, należy przypisać wartość **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="24a4f-139">In SAP Business ByDesign, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="24a4f-140">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SAP Business ByDesign, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="24a4f-140">To configure and test Azure AD single sign-on with SAP Business ByDesign, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="24a4f-141">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configure-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="24a4f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="24a4f-142">**[Tworzenie użytkownika testowego usługi Azure AD](#create-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="24a4f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="24a4f-143">**[Tworzenie użytkownika testowego SAP Business ByDesign](#create-an-sap-business-bydesign-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta SAP Business ByDesign, połączonej z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="24a4f-143">**[Create an SAP Business ByDesign test user](#create-an-sap-business-bydesign-test-user)** - to have a counterpart of Britta Simon in SAP Business ByDesign that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="24a4f-144">**[Przypisz użytkownika testowego usługi Azure AD](#assign-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="24a4f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="24a4f-145">**[Test rejestracji jednokrotnej](#test-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="24a4f-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="24a4f-146">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="24a4f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="24a4f-147">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne do aplikacji SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="24a4f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP Business ByDesign application.</span></span>

<span data-ttu-id="24a4f-148">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z SAP Business ByDesign, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="24a4f-148">**To configure Azure AD single sign-on with SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="24a4f-149">W portalu Azure na **SAP Business ByDesign** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="24a4f-149">In the Azure portal, on the **SAP Business ByDesign** application integration page, click **Single sign-on**.</span></span>

    ![Skonfigurować łącze rejestracji jednokrotnej][4]

2. <span data-ttu-id="24a4f-151">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="24a4f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_samlbase.png)

3. <span data-ttu-id="24a4f-153">Na **adresy URL i SAP Business ByDesign domeny** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="24a4f-153">On the **SAP Business ByDesign Domain and URLs** section, perform the following steps:</span></span>

    ![Adresy URL i SAP Business ByDesign domeny pojedynczy informacje logowania jednokrotnego](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_url.png)

    <span data-ttu-id="24a4f-155">a.</span><span class="sxs-lookup"><span data-stu-id="24a4f-155">a.</span></span> <span data-ttu-id="24a4f-156">W **adres URL logowania** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="24a4f-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span></span>

    <span data-ttu-id="24a4f-157">b.</span><span class="sxs-lookup"><span data-stu-id="24a4f-157">b.</span></span> <span data-ttu-id="24a4f-158">W **identyfikator** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<servername>.sapbydesign.com`</span><span class="sxs-lookup"><span data-stu-id="24a4f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<servername>.sapbydesign.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="24a4f-159">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="24a4f-159">These values are not real.</span></span> <span data-ttu-id="24a4f-160">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="24a4f-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="24a4f-161">Skontaktuj się z [zespołem pomocy technicznej SAP Business ByDesign klienta](https://www.sap.com/products/cloud-analytics.support.html) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="24a4f-161">Contact [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to get these values.</span></span>

4. <span data-ttu-id="24a4f-162">Na **atrybuty użytkownika** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="24a4f-162">On the **User Attributes** section, perform the following steps:</span></span>

    ![SAP Business ByDesign atrybutów sekcji](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_attribute.png)
    
    <span data-ttu-id="24a4f-164">a.</span><span class="sxs-lookup"><span data-stu-id="24a4f-164">a.</span></span> <span data-ttu-id="24a4f-165">W **identyfikator użytkownika** listy, wybierz **ExtractMailPrefix()** funkcji.</span><span class="sxs-lookup"><span data-stu-id="24a4f-165">In **User Identifier** list, select the **ExtractMailPrefix()** function.</span></span>
    
    <span data-ttu-id="24a4f-166">b.</span><span class="sxs-lookup"><span data-stu-id="24a4f-166">b.</span></span> <span data-ttu-id="24a4f-167">Z **poczty** wybierz atrybut użytkownika, którego chcesz użyć implementacji.</span><span class="sxs-lookup"><span data-stu-id="24a4f-167">From the **Mail** list, select the user attribute you want to use for your implementation.</span></span> <span data-ttu-id="24a4f-168">Na przykład jeśli ma być używany jako identyfikator użytkownika unikatowy identyfikator pracownika, a wartość atrybutu są przechowywane w ExtensionAttribute2, wybierz user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="24a4f-168">For example, if you want to use the EmployeeID as unique user identifier and you have stored the attribute value in the ExtensionAttribute2, then select user.extensionattribute2.</span></span>     

5. <span data-ttu-id="24a4f-169">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="24a4f-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_certificate.png) 

6. <span data-ttu-id="24a4f-171">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="24a4f-171">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="24a4f-173">Na **SAP Business ByDesign konfiguracji** kliknij **skonfigurować SAP Business ByDesign** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="24a4f-173">On the **SAP Business ByDesign Configuration** section, click **Configure SAP Business ByDesign** to open **Configure sign-on** window.</span></span> <span data-ttu-id="24a4f-174">Kopiuj **SAML pojedynczy znak na adres URL usługi** z **sekcji krótkimi opisami.**</span><span class="sxs-lookup"><span data-stu-id="24a4f-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![SAP Business ByDesign konfiguracji](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_configure.png) 

8. <span data-ttu-id="24a4f-176">Aby uzyskać logowania jednokrotnego skonfigurowane dla aplikacji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="24a4f-176">To get SSO configured for your application, perform the following steps:</span></span>
   
    <span data-ttu-id="24a4f-177">a.</span><span class="sxs-lookup"><span data-stu-id="24a4f-177">a.</span></span> <span data-ttu-id="24a4f-178">Zaloguj się do portalu usługi SAP Business ByDesign z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="24a4f-178">Sign on to your SAP Business ByDesign portal with administrator rights.</span></span>
   
    <span data-ttu-id="24a4f-179">b.</span><span class="sxs-lookup"><span data-stu-id="24a4f-179">b.</span></span> <span data-ttu-id="24a4f-180">Przejdź do **aplikacji i typowych zadań zarządzania użytkownika** i kliknij przycisk **dostawcy tożsamości** kartę.</span><span class="sxs-lookup"><span data-stu-id="24a4f-180">Navigate to **Application and User Management Common Task** and click the **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="24a4f-181">c.</span><span class="sxs-lookup"><span data-stu-id="24a4f-181">c.</span></span> <span data-ttu-id="24a4f-182">Kliknij przycisk **nowego dostawcy tożsamości** i wybierz plik XML metadanych, który został pobrany z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="24a4f-182">Click **New Identity Provider** and select the metadata XML file that you have downloaded from the Azure portal.</span></span> <span data-ttu-id="24a4f-183">Przez importowanie metadanych, system automatycznie wysyła certyfikat wymagany podpis, jak i certyfikat szyfrowania.</span><span class="sxs-lookup"><span data-stu-id="24a4f-183">By importing the metadata, the system automatically uploads the required signature certificate and encryption certificate.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_54.png)
   
    <span data-ttu-id="24a4f-185">d.</span><span class="sxs-lookup"><span data-stu-id="24a4f-185">d.</span></span> <span data-ttu-id="24a4f-186">Aby uwzględnić **adres URL usługi klienta potwierdzenia** do żądania SAML, wybierz **zawierają potwierdzenie konsumenta adres URL usługi**.</span><span class="sxs-lookup"><span data-stu-id="24a4f-186">To include the **Assertion Consumer Service URL** into the SAML request, select **Include Assertion Consumer Service URL**.</span></span>
   
    <span data-ttu-id="24a4f-187">e.</span><span class="sxs-lookup"><span data-stu-id="24a4f-187">e.</span></span> <span data-ttu-id="24a4f-188">Kliknij przycisk **aktywacji rejestracji jednokrotnej**.</span><span class="sxs-lookup"><span data-stu-id="24a4f-188">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="24a4f-189">f.</span><span class="sxs-lookup"><span data-stu-id="24a4f-189">f.</span></span> <span data-ttu-id="24a4f-190">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="24a4f-190">Save your changes.</span></span>
   
    <span data-ttu-id="24a4f-191">g.</span><span class="sxs-lookup"><span data-stu-id="24a4f-191">g.</span></span> <span data-ttu-id="24a4f-192">Kliknij przycisk **systemie** kartę.</span><span class="sxs-lookup"><span data-stu-id="24a4f-192">Click the **My System** tab.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_52.png)
   
    <span data-ttu-id="24a4f-194">h.</span><span class="sxs-lookup"><span data-stu-id="24a4f-194">h.</span></span> <span data-ttu-id="24a4f-195">Wklej **SAML pojedynczy znak na adres URL usługi**, która została skopiowana z portalu Azure do **Azure AD znaku w adresie URL** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="24a4f-195">Paste **SAML Single Sign-On Service URL**, which you have copied from the Azure portal it into the **Azure AD Sign On URL** textbox.</span></span>
   
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_53.png)
   
    <span data-ttu-id="24a4f-197">i.</span><span class="sxs-lookup"><span data-stu-id="24a4f-197">i.</span></span> <span data-ttu-id="24a4f-198">Określ, czy pracownik może ręcznie wybrać między zalogowanie się przy użyciu Identyfikatora użytkownika i hasła lub logowania jednokrotnego, wybierając **wybór dostawcy tożsamości ręcznego**.</span><span class="sxs-lookup"><span data-stu-id="24a4f-198">Specify whether the employee can manually choose between logging on with user ID and password or SSO by selecting **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="24a4f-199">j.</span><span class="sxs-lookup"><span data-stu-id="24a4f-199">j.</span></span> <span data-ttu-id="24a4f-200">W **adres URL logowania jednokrotnego** sekcji, podaj adres URL, które mają być używane przez pracowników do logowania się do systemu.</span><span class="sxs-lookup"><span data-stu-id="24a4f-200">In the **SSO URL** section, specify the URL that should be used by the employee to logon to the system.</span></span> 
    <span data-ttu-id="24a4f-201">W URL wysyłane do listy rozwijanej pracownika można wybrać jedną z następujących opcji:</span><span class="sxs-lookup"><span data-stu-id="24a4f-201">In the URL Sent to Employee dropdown list, you can choose between the following options:</span></span>
   
    <span data-ttu-id="24a4f-202">**Adres URL — Usługa rejestracji Jednokrotnej**</span><span class="sxs-lookup"><span data-stu-id="24a4f-202">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="24a4f-203">System wysyła tylko adres URL normalne systemu do pracownika.</span><span class="sxs-lookup"><span data-stu-id="24a4f-203">The system sends only the normal system URL to the employee.</span></span> <span data-ttu-id="24a4f-204">Pracownik nie może zalogować się przy użyciu logowania jednokrotnego i musi użyć hasła lub zamiast tego certyfikatu.</span><span class="sxs-lookup"><span data-stu-id="24a4f-204">The employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="24a4f-205">**ADRES URL LOGOWANIA JEDNOKROTNEGO**</span><span class="sxs-lookup"><span data-stu-id="24a4f-205">**SSO URL**</span></span> 
   
    <span data-ttu-id="24a4f-206">System wysyła tylko adres URL logowania jednokrotnego do pracownika.</span><span class="sxs-lookup"><span data-stu-id="24a4f-206">The system sends only the SSO URL to the employee.</span></span> <span data-ttu-id="24a4f-207">Pracownik może zalogować się przy użyciu logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="24a4f-207">The employee can log on using SSO.</span></span> <span data-ttu-id="24a4f-208">Żądanie uwierzytelnienia jest przekierowywane przez dostawców tożsamości.</span><span class="sxs-lookup"><span data-stu-id="24a4f-208">Authentication request is redirected through the IdP.</span></span>
   
    <span data-ttu-id="24a4f-209">**Automatyczne wybieranie**</span><span class="sxs-lookup"><span data-stu-id="24a4f-209">**Automatic Selection**</span></span>
   
    <span data-ttu-id="24a4f-210">Jeśli logowania jednokrotnego nie jest aktywne, system wysyła system normalny adres URL do pracownika.</span><span class="sxs-lookup"><span data-stu-id="24a4f-210">If SSO is not active, the system sends the normal system URL to the employee.</span></span> <span data-ttu-id="24a4f-211">Jeśli usługa rejestracji Jednokrotnej jest aktywny, system sprawdza, czy pracownik ma hasło.</span><span class="sxs-lookup"><span data-stu-id="24a4f-211">If SSO is active, the system checks whether the employee has a password.</span></span> <span data-ttu-id="24a4f-212">Jeśli hasło jest dostępny, zarówno adres URL logowania jednokrotnego i adres URL logowania jednokrotnego nie są wysyłane do pracownika.</span><span class="sxs-lookup"><span data-stu-id="24a4f-212">If a password is available, both SSO URL and Non-SSO URL are sent to the employee.</span></span> <span data-ttu-id="24a4f-213">Jeśli pracownik nie ma hasła, adres URL logowania jednokrotnego są wysyłane do pracownika.</span><span class="sxs-lookup"><span data-stu-id="24a4f-213">However, if the employee has no password, only the SSO URL is sent to the employee.</span></span>
   
    <span data-ttu-id="24a4f-214">k.</span><span class="sxs-lookup"><span data-stu-id="24a4f-214">k.</span></span> <span data-ttu-id="24a4f-215">Zapisz zmiany.</span><span class="sxs-lookup"><span data-stu-id="24a4f-215">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="24a4f-216">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="24a4f-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="24a4f-217">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="24a4f-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="24a4f-218">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="24a4f-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="24a4f-219">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="24a4f-219">Create an Azure AD test user</span></span>

<span data-ttu-id="24a4f-220">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="24a4f-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Tworzenie użytkownika testowego usługi Azure AD][100]

<span data-ttu-id="24a4f-222">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="24a4f-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="24a4f-223">W portalu Azure, w okienku po lewej stronie kliknij **usługi Azure Active Directory** przycisku.</span><span class="sxs-lookup"><span data-stu-id="24a4f-223">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="24a4f-225">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="24a4f-225">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="24a4f-227">Aby otworzyć **użytkownika** okno dialogowe, kliknij przycisk **Dodaj** w górnej części **wszyscy użytkownicy** okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="24a4f-227">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Przycisk Dodaj](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="24a4f-229">W **użytkownika** okna dialogowego wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="24a4f-229">In the **User** dialog box, perform the following steps:</span></span>

    ![Okno dialogowe użytkownika](./media/active-directory-saas-sapbusinessbydesign-tutorial/create_aaduser_04.png)

    <span data-ttu-id="24a4f-231">a.</span><span class="sxs-lookup"><span data-stu-id="24a4f-231">a.</span></span> <span data-ttu-id="24a4f-232">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="24a4f-232">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="24a4f-233">b.</span><span class="sxs-lookup"><span data-stu-id="24a4f-233">b.</span></span> <span data-ttu-id="24a4f-234">W **nazwy użytkownika** wpisz adres e-mail użytkownika Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="24a4f-234">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="24a4f-235">c.</span><span class="sxs-lookup"><span data-stu-id="24a4f-235">c.</span></span> <span data-ttu-id="24a4f-236">Wybierz **Pokaż hasło** pole wyboru, a następnie zanotuj wartość, która jest wyświetlana w **hasło** pole.</span><span class="sxs-lookup"><span data-stu-id="24a4f-236">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="24a4f-237">d.</span><span class="sxs-lookup"><span data-stu-id="24a4f-237">d.</span></span> <span data-ttu-id="24a4f-238">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="24a4f-238">Click **Create**.</span></span>
 
### <a name="create-an-sap-business-bydesign-test-user"></a><span data-ttu-id="24a4f-239">Tworzenie użytkownika testowego SAP Business ByDesign</span><span class="sxs-lookup"><span data-stu-id="24a4f-239">Create an SAP Business ByDesign test user</span></span>

<span data-ttu-id="24a4f-240">W tej sekcji należy utworzyć użytkownika o nazwie Simona Britta w SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="24a4f-240">In this section, you create a user called Britta Simon in SAP Business ByDesign.</span></span> <span data-ttu-id="24a4f-241">We współpracy z [zespołem pomocy technicznej SAP Business ByDesign klienta](https://www.sap.com/products/cloud-analytics.support.html) Aby dodać użytkowników do platformy SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="24a4f-241">Please work with [SAP Business ByDesign Client support team](https://www.sap.com/products/cloud-analytics.support.html) to add the users in the SAP Business ByDesign platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="24a4f-242">Upewnij się, że wartość NameID powinna być zgodna z pola Nazwa użytkownika na platformie programu SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="24a4f-242">Please make sure that NameID value should match with the username field in the SAP Business ByDesign platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="24a4f-243">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="24a4f-243">Assign the Azure AD test user</span></span>

<span data-ttu-id="24a4f-244">W tej sekcji musisz włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do programu SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="24a4f-244">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP Business ByDesign.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="24a4f-246">**Aby przypisać Simona Britta SAP Business ByDesign, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="24a4f-246">**To assign Britta Simon to SAP Business ByDesign, perform the following steps:**</span></span>

1. <span data-ttu-id="24a4f-247">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="24a4f-247">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="24a4f-249">Na liście aplikacji zaznacz **SAP Business ByDesign**.</span><span class="sxs-lookup"><span data-stu-id="24a4f-249">In the applications list, select **SAP Business ByDesign**.</span></span>

    ![Łącze SAP Business ByDesign na liście aplikacji](./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_sapbusinessbydesign_app.png)  

3. <span data-ttu-id="24a4f-251">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="24a4f-251">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202]

4. <span data-ttu-id="24a4f-253">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="24a4f-253">Click **Add** button.</span></span> <span data-ttu-id="24a4f-254">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="24a4f-254">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="24a4f-256">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="24a4f-256">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="24a4f-257">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="24a4f-257">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="24a4f-258">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="24a4f-258">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="24a4f-259">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="24a4f-259">Test single sign-on</span></span>

<span data-ttu-id="24a4f-260">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="24a4f-260">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="24a4f-261">Po kliknięciu kafelka SAP Business ByDesign w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji SAP Business ByDesign.</span><span class="sxs-lookup"><span data-stu-id="24a4f-261">When you click the SAP Business ByDesign tile in the Access Panel, you should get automatically signed-on to your SAP Business ByDesign application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="24a4f-262">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="24a4f-262">Additional resources</span></span>

* [<span data-ttu-id="24a4f-263">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="24a4f-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="24a4f-264">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="24a4f-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sapbusinessbydesign-tutorial/tutorial_general_203.png

