---
title: 'Samouczek: Integracji Azure Active Directory z HR2day przez Merces | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i HR2day przez Merces."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 77e2fcf9c306259286b15767f3a992510d6d79d8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a><span data-ttu-id="ef802-103">Samouczek: Integracji Azure Active Directory z HR2day przez Merces</span><span class="sxs-lookup"><span data-stu-id="ef802-103">Tutorial: Azure Active Directory integration with HR2day by Merces</span></span>

<span data-ttu-id="ef802-104">Z tego samouczka dowiesz się integrowanie HR2day przez Merces z usługi Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ef802-104">In this tutorial, you learn how to integrate HR2day by Merces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ef802-105">Integracja z usługą Azure AD HR2day przez Merces zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="ef802-105">Integrating HR2day by Merces with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ef802-106">Można kontrolować w usłudze Azure AD, który ma dostęp do HR2day przez Merces.</span><span class="sxs-lookup"><span data-stu-id="ef802-106">You can control in Azure AD who has access to HR2day by Merces.</span></span>
- <span data-ttu-id="ef802-107">Można umożliwić użytkownikom automatycznie pobrać zalogujesz się HR2day przy Merces z konta usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef802-107">You can enable your users to automatically get signed in to HR2day by Merces with their Azure AD accounts.</span></span>
- <span data-ttu-id="ef802-108">Możesz zarządzać kont w jednej centralnej lokalizacji--portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="ef802-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="ef802-109">Aby uzyskać więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ef802-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef802-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="ef802-110">Prerequisites</span></span>

<span data-ttu-id="ef802-111">Aby skonfigurować integrację usługi Azure AD z HR2day przez Merces, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="ef802-111">To configure Azure AD integration with HR2day by Merces, you need the following items:</span></span>

- <span data-ttu-id="ef802-112">Subskrypcja usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef802-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="ef802-113">HR2day przez Merces logowanie jednokrotne włączone subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ef802-113">An HR2day by Merces single sign-on enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="ef802-114">Nie zaleca się używanie środowiska produkcyjnego do testowania czynności w tym samouczku.</span><span class="sxs-lookup"><span data-stu-id="ef802-114">We don't recommend using a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="ef802-115">Aby przetestować kroki opisane w tym samouczku, wykonaj te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="ef802-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="ef802-116">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="ef802-116">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="ef802-117">Pobierz [miesięczna bezpłatna wersja próbna usługi Azure AD](https://azure.microsoft.com/pricing/free-trial/) Jeśli jeszcze nie masz.</span><span class="sxs-lookup"><span data-stu-id="ef802-117">Get a [one-month free trial of Azure AD](https://azure.microsoft.com/pricing/free-trial/) if you don't already have it.</span></span>  

## <a name="scenario-description"></a><span data-ttu-id="ef802-118">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="ef802-118">Scenario description</span></span>
<span data-ttu-id="ef802-119">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="ef802-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ef802-120">Scenariusz, który jest opisana w tym temacie składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="ef802-120">The scenario that's outlined here consists of two main building blocks:</span></span>

1. <span data-ttu-id="ef802-121">Dodawanie HR2day przez Merces z galerii.</span><span class="sxs-lookup"><span data-stu-id="ef802-121">Adding HR2day by Merces from the gallery.</span></span>
2. <span data-ttu-id="ef802-122">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="ef802-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-hr2day-by-merces-from-the-gallery"></a><span data-ttu-id="ef802-123">Dodaj HR2day przez Merces z galerii</span><span class="sxs-lookup"><span data-stu-id="ef802-123">Add HR2day by Merces from the gallery</span></span>
<span data-ttu-id="ef802-124">Aby skonfigurować integrację usługi Azure AD HR2day przez Merces, należy dodać HR2day przez Merces z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="ef802-124">To configure the integration of HR2day by Merces into Azure AD, add HR2day by Merces from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ef802-125">**Aby dodać HR2day przez Merces z galerii, należy wykonać następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ef802-125">**To add HR2day by Merces from the gallery, take the following steps:**</span></span>

1. <span data-ttu-id="ef802-126">W [portalu Azure](https://portal.azure.com), w okienku nawigacji po lewej stronie wybierz **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ef802-126">In the [Azure portal](https://portal.azure.com), on the left navigation pane, select the **Azure Active Directory** icon.</span></span> 

    ![Usługa Active Directory][1]

2. <span data-ttu-id="ef802-128">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ef802-128">Go to **Enterprise applications**.</span></span> <span data-ttu-id="ef802-129">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ef802-129">Then go to **All applications**.</span></span>

    ![Aplikacje][2]
    
3. <span data-ttu-id="ef802-131">Aby dodać nową aplikację, zaznacz **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ef802-131">To add a new application, select the **New application** button on the top of the dialog box.</span></span>

    ![Aplikacje][3]

4. <span data-ttu-id="ef802-133">W polu wyszukiwania wpisz **HR2day przez Merces**.</span><span class="sxs-lookup"><span data-stu-id="ef802-133">In the search box, type **HR2day by Merces**.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. <span data-ttu-id="ef802-135">W panelu wyników wybierz **HR2day przez Merces**, a następnie wybierz **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="ef802-135">In the results panel, select **HR2day by Merces**, and then select the **Add** button to add the application.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="ef802-137">Konfiguracja i testowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ef802-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="ef802-138">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z HR2day przez Merces oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="ef802-138">In this section, you configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ef802-139">Do rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, komu użytkownika odpowiednika w HR2day przez Merces jest użytkownikiem w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef802-139">For single sign-on to work, Azure AD needs to know who the counterpart user in HR2day by Merces is to a user in Azure AD.</span></span> <span data-ttu-id="ef802-140">Innymi słowy należy ustanowić powiązanie użytkownika usługi Azure AD i danemu użytkownikowi w HR2day przez Merces.</span><span class="sxs-lookup"><span data-stu-id="ef802-140">In other words, you need to establish a link between an Azure AD user and the related user in HR2day by Merces.</span></span>

<span data-ttu-id="ef802-141">HR2day przez Merces, przypisywanie **nazwy użytkownika** w usłudze Azure AD do **Username** ustanowienie relacji.</span><span class="sxs-lookup"><span data-stu-id="ef802-141">In HR2day by Merces, assign the **user name** in Azure AD to  **Username** to establish the relationship.</span></span>

<span data-ttu-id="ef802-142">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z HR2day przez Merces, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="ef802-142">To configure and test Azure AD single sign-on with HR2day by Merces, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ef802-143">[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on): umożliwianie użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="ef802-143">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on): Enable your users to use this feature.</span></span>
2. <span data-ttu-id="ef802-144">[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user): Test usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ef802-144">[Create an Azure AD test user](#creating-an-azure-ad-test-user): Test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ef802-145">[Utwórz HR2day przez użytkownika testowego Merces](#creating-an-hr2day-by-merces-test-user): tworzenie odpowiednikiem Simona Britta w HR2day przez Merces połączonego z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ef802-145">[Create an HR2day by Merces test user](#creating-an-hr2day-by-merces-test-user): Create a counterpart of Britta Simon in HR2day by Merces that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ef802-146">[Przypisz użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user): Włącz Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ef802-146">[Assign the Azure AD test user](#assigning-the-azure-ad-test-user): Enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ef802-147">[Test rejestracji jednokrotnej](#testing-single-sign-on): Sprawdź, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="ef802-147">[Test single sign-on](#testing-single-sign-on): Verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="ef802-148">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ef802-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="ef802-149">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i konfigurowanie rejestracji jednokrotnej w sieci HR2day przez aplikację Merces.</span><span class="sxs-lookup"><span data-stu-id="ef802-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HR2day by Merces application.</span></span>

<span data-ttu-id="ef802-150">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z HR2day przez Merces, należy wykonać następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ef802-150">**To configure Azure AD single sign-on with HR2day by Merces, take the following steps:**</span></span>

1. <span data-ttu-id="ef802-151">W portalu Azure na **HR2day przez Merces** strona integracji aplikacji, wybierz opcję **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="ef802-151">In the Azure portal, on the **HR2day by Merces** application integration page, select **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="ef802-153">Aby włączyć logowanie jednokrotne, w **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego**.</span><span class="sxs-lookup"><span data-stu-id="ef802-153">To enable single sign-on, in the **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. <span data-ttu-id="ef802-155">W **HR2day Merces domeny i adresy URL** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ef802-155">In the **HR2day by Merces Domain and URLs** section, take the following steps:</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    <span data-ttu-id="ef802-157">a.</span><span class="sxs-lookup"><span data-stu-id="ef802-157">a.</span></span> <span data-ttu-id="ef802-158">W **adres URL logowania** wpisz adres URL przy użyciu następującego wzorca: `https://<tenantname>.force.com/<instancename>`.</span><span class="sxs-lookup"><span data-stu-id="ef802-158">In the **Sign-on URL** box, type a URL by using the following pattern: `https://<tenantname>.force.com/<instancename>`.</span></span>

    <span data-ttu-id="ef802-159">b.</span><span class="sxs-lookup"><span data-stu-id="ef802-159">b.</span></span> <span data-ttu-id="ef802-160">W **identyfikator** wpisz adres URL przy użyciu następującego wzorca: `https://hr2day.force.com/<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="ef802-160">In the **Identifier** box, type a URL by using the following pattern: `https://hr2day.force.com/<companyname>`.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ef802-161">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="ef802-161">These values are not real.</span></span> <span data-ttu-id="ef802-162">Rzeczywisty adres URL logowania i identyfikator, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="ef802-162">Update these values with the actual sign-on URL and identifier.</span></span> <span data-ttu-id="ef802-163">Skontaktuj się z [HR2day przez zespół pomocy technicznej klienta Merces](mailto:servicedesk@merces.nl) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="ef802-163">Contact the [HR2day by Merces client support team](mailto:servicedesk@merces.nl) to get these values.</span></span> 
 


4. <span data-ttu-id="ef802-164">Na **certyfikat podpisywania SAML** wybierz opcję **Certificate(Base64)**, a następnie zapisz plik certyfikatu na komputerze.</span><span class="sxs-lookup"><span data-stu-id="ef802-164">On the **SAML Signing Certificate** section, select **Certificate(Base64)**, and then save the certificate file on your computer.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. <span data-ttu-id="ef802-166">W tej sekcji opisano sposób umożliwić użytkownikom uwierzytelnianie na HR2day przez Merces do swojego konta w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef802-166">This section describes how to enable users to authenticate to HR2day by Merces with their account in Azure AD.</span></span> <span data-ttu-id="ef802-167">One to robić przy użyciu Federacji, która jest oparta na protokole SAML.</span><span class="sxs-lookup"><span data-stu-id="ef802-167">They do this by using federation that's based on the SAML protocol.</span></span>

    <span data-ttu-id="ef802-168">Twoje HR2day przez aplikację Merces oczekuje potwierdzenia języka SAML w określonym formacie, który wymaga można dodać mapowanie atrybutów niestandardowych do Twojego tokenu SAML.</span><span class="sxs-lookup"><span data-stu-id="ef802-168">Your HR2day by Merces application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token.</span></span> <span data-ttu-id="ef802-169">Poniższy zrzut ekranu przedstawia przykład.</span><span class="sxs-lookup"><span data-stu-id="ef802-169">The following screenshot shows an example of this.</span></span> 

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    <span data-ttu-id="ef802-171">Aby można było skonfigurować potwierdzenia języka SAML, należy skontaktować się [HR2day przez zespół pomocy technicznej klienta Merces](mailto:servicedesk@merces.nl) i zażądać wartość atrybutu Unikatowy identyfikator dla dzierżawy.</span><span class="sxs-lookup"><span data-stu-id="ef802-171">Before you can configure the SAML assertion, you must contact the [HR2day by Merces Client support team](mailto:servicedesk@merces.nl) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="ef802-172">Należy tę wartość, aby wykonać kroki opisane w następnej sekcji.</span><span class="sxs-lookup"><span data-stu-id="ef802-172">You need this value to complete the steps in the next section.</span></span> 

6. <span data-ttu-id="ef802-173">W **logowanie jednokrotne** okna dialogowego, **atrybuty użytkownika** skonfiguruj atrybut tokenu SAML, jak pokazano na poniższej ilustracji.</span><span class="sxs-lookup"><span data-stu-id="ef802-173">In the **Single sign-on** dialog box, in the **User Attributes** section, configure the SAML token attribute as shown in the following image.</span></span> <span data-ttu-id="ef802-174">Następnie należy wykonać następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="ef802-174">Then take the following steps.</span></span>
    
      | <span data-ttu-id="ef802-175">Nazwa atrybutu</span><span class="sxs-lookup"><span data-stu-id="ef802-175">Attribute name</span></span>    |   <span data-ttu-id="ef802-176">Wartość atrybutu</span><span class="sxs-lookup"><span data-stu-id="ef802-176">Attribute value</span></span> |  
    | ------------------- | -------------------- |    
    | <span data-ttu-id="ef802-177">ATTR_LOGINCLAIM</span><span class="sxs-lookup"><span data-stu-id="ef802-177">ATTR_LOGINCLAIM</span></span> | <span data-ttu-id="ef802-178">sprzężenia ([poczty] "102938475Z", "@"</span><span class="sxs-lookup"><span data-stu-id="ef802-178">join([mail],"102938475Z","@"</span></span> |
    
      <span data-ttu-id="ef802-179">a.</span><span class="sxs-lookup"><span data-stu-id="ef802-179">a.</span></span> <span data-ttu-id="ef802-180">Aby otworzyć **Dodawanie atrybutu** okno dialogowe, wybierz opcję **Dodaj atrybut**.</span><span class="sxs-lookup"><span data-stu-id="ef802-180">To open the **Add Attribute** dialog, select **Add attribute**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="ef802-183">b.</span><span class="sxs-lookup"><span data-stu-id="ef802-183">b.</span></span> <span data-ttu-id="ef802-184">W **nazwa** wpisz **ATTR_LOGINCLAIM**.</span><span class="sxs-lookup"><span data-stu-id="ef802-184">In the **Name** box, type **ATTR_LOGINCLAIM**.</span></span>

    <span data-ttu-id="ef802-185">c.</span><span class="sxs-lookup"><span data-stu-id="ef802-185">c.</span></span> <span data-ttu-id="ef802-186">Z **wartość** listy, wybierz **Join()**.</span><span class="sxs-lookup"><span data-stu-id="ef802-186">From the **Value** list, select **Join()**.</span></span>

    <span data-ttu-id="ef802-187">d.</span><span class="sxs-lookup"><span data-stu-id="ef802-187">d.</span></span> <span data-ttu-id="ef802-188">Z **ciąg1** listy, wybierz **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="ef802-188">From the **String1** list, select **user.mail**.</span></span>

    <span data-ttu-id="ef802-189">e.</span><span class="sxs-lookup"><span data-stu-id="ef802-189">e.</span></span> <span data-ttu-id="ef802-190">Aby uzyskać **ciąg2**, wpisz unikatowy identyfikator, który jest świadczona przez Twojego zespołu HR2day.</span><span class="sxs-lookup"><span data-stu-id="ef802-190">For **String2**, type the unique identifier that's provided by your HR2day team.</span></span>

    <span data-ttu-id="ef802-191">f.</span><span class="sxs-lookup"><span data-stu-id="ef802-191">f.</span></span> <span data-ttu-id="ef802-192">W **separatora** wpisz  **@** .</span><span class="sxs-lookup"><span data-stu-id="ef802-192">In the **Separator** box, type **@**.</span></span>
    
    <span data-ttu-id="ef802-193">g.</span><span class="sxs-lookup"><span data-stu-id="ef802-193">g.</span></span> <span data-ttu-id="ef802-194">Wybierz **Ok**.</span><span class="sxs-lookup"><span data-stu-id="ef802-194">Select **Ok**.</span></span>

7. <span data-ttu-id="ef802-195">Wybierz ikonę **Zapisz**.</span><span class="sxs-lookup"><span data-stu-id="ef802-195">Select the **Save** button.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="ef802-197">W **HR2day przez konfigurację Merces** zaznacz **skonfigurować HR2day przez Merces** otworzyć **Konfigurowanie logowania jednokrotnego** okna.</span><span class="sxs-lookup"><span data-stu-id="ef802-197">In the **HR2day by Merces Configuration** section, select **Configure HR2day by Merces** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="ef802-198">Kopiuj **Sign-Out adres URL**, **SAML identyfikator jednostki**, i **SAML pojedynczy znak na adres URL usługi** z **krótkimi opisami** sekcji.</span><span class="sxs-lookup"><span data-stu-id="ef802-198">Copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference** section.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. <span data-ttu-id="ef802-200">Aby skonfigurować logowanie Jednokrotne dla aplikacji, skontaktuj się z [HR2day przez zespół pomocy technicznej klienta Merces](mailTo:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="ef802-200">To configure SSO  for your application, contact the [HR2day by Merces client support team](mailTo:servicedesk@merces.nl).</span></span> <span data-ttu-id="ef802-201">Dołącz pobrany **Certificate(Base64)** pliku do wiadomości e-mail.</span><span class="sxs-lookup"><span data-stu-id="ef802-201">Attach the downloaded **Certificate(Base64)** file to your email.</span></span> <span data-ttu-id="ef802-202">Udostępniają **Sign-Out URL**, **identyfikator jednostki SAML**, i **SAML pojedynczy znak na adres URL usługi** tak, aby można je skonfigurować integracji logowania jednokrotnego.</span><span class="sxs-lookup"><span data-stu-id="ef802-202">Also provide the **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** so that they can be configured for SSO integration.</span></span>

    > [!NOTE]
    ><span data-ttu-id="ef802-203">Wspomina do zespołu Merces, że integracja wymaga identyfikator jednostki można ustawić za pomocą wzorca **https://hr2day.force.com/INSTANCENAME**.</span><span class="sxs-lookup"><span data-stu-id="ef802-203">Mention to the Merces team that this integration needs the Entity ID to be set with the pattern **https://hr2day.force.com/INSTANCENAME**.</span></span>

    > [!TIP]
    ><span data-ttu-id="ef802-204">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="ef802-204">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ef802-205">Po dodaniu tej aplikacji z **usługi Active Directory** > **aplikacje dla przedsiębiorstw** zaznacz **rejestracji jednokrotnej** kartę.</span><span class="sxs-lookup"><span data-stu-id="ef802-205">After you add this app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab.</span></span> <span data-ttu-id="ef802-206">Dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="ef802-206">Then access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ef802-207">Więcej o funkcji dokumentacji osadzony w [usługi Azure AD osadzonych dokumentacji]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="ef802-207">You can read more about the embedded documentation feature in the [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="ef802-208">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef802-208">Create an Azure AD test user</span></span>
<span data-ttu-id="ef802-209">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="ef802-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="ef802-211">**Aby utworzyć użytkownika testowego w usłudze Azure AD, należy wykonać następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ef802-211">**To create a test user in Azure AD, take the following steps:**</span></span>

1. <span data-ttu-id="ef802-212">W **portalu Azure**, w okienku nawigacji po lewej stronie wybierz **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="ef802-212">In the **Azure portal**, on the left navigation pane, select the **Azure Active Directory** icon.</span></span>

    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ef802-214">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup**, a następnie wybierz **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="ef802-214">To display the list of users, go to **Users and groups**, and then select **All users**.</span></span>
    
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ef802-216">Aby otworzyć **użytkownika** okno dialogowe, wybierz opcję **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="ef802-216">To open the **User** dialog box, select **Add** on the top of the dialog box.</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ef802-218">W **użytkownika** okna dialogowego należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="ef802-218">In the **User** dialog box, take the following steps:</span></span>
 
    ![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ef802-220">a.</span><span class="sxs-lookup"><span data-stu-id="ef802-220">a.</span></span> <span data-ttu-id="ef802-221">W **nazwa** wpisz **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ef802-221">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ef802-222">b.</span><span class="sxs-lookup"><span data-stu-id="ef802-222">b.</span></span> <span data-ttu-id="ef802-223">W **nazwy użytkownika** wpisz **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ef802-223">In the **User name** box, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ef802-224">c.</span><span class="sxs-lookup"><span data-stu-id="ef802-224">c.</span></span> <span data-ttu-id="ef802-225">Wybierz **Pokaż hasło**, a następnie Zapisz hasło.</span><span class="sxs-lookup"><span data-stu-id="ef802-225">Select **Show Password**, and then write down the password.</span></span>

    <span data-ttu-id="ef802-226">d.</span><span class="sxs-lookup"><span data-stu-id="ef802-226">d.</span></span> <span data-ttu-id="ef802-227">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="ef802-227">Select **Create**.</span></span>
 
### <a name="create-an-hr2day-by-merces-test-user"></a><span data-ttu-id="ef802-228">Utwórz HR2day przez Merces użytkownika testowego</span><span class="sxs-lookup"><span data-stu-id="ef802-228">Create an HR2day by Merces test user</span></span>

<span data-ttu-id="ef802-229">Celem tej sekcji jest utworzenie użytkownika o nazwie Simona Britta w HR2day przez Merces.</span><span class="sxs-lookup"><span data-stu-id="ef802-229">The objective of this section is to create a user called Britta Simon in HR2day by Merces.</span></span> <span data-ttu-id="ef802-230">Aby dodać użytkowników w ramach konta HR2day, pracy z [HR2day przez zespół pomocy technicznej klienta Merces](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="ef802-230">To add the users in the HR2day account, work with the [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span> 

> [!NOTE]
> <span data-ttu-id="ef802-231">Jeśli trzeba ręcznie utworzyć użytkownika, skontaktuj się z [HR2day przez zespół pomocy technicznej klienta Merces](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="ef802-231">If you need to create a user manually, contact the [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="ef802-232">Przypisz użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef802-232">Assign the Azure AD test user</span></span>

<span data-ttu-id="ef802-233">W tej sekcji można włączyć Simona Britta do udostępnienia jej HR2day przez Merces za pomocą usługi Azure rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="ef802-233">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to HR2day by Merces.</span></span>

![Przypisz użytkownika][200] 

<span data-ttu-id="ef802-235">**Aby przypisać Simona Britta HR2day przez Merces, należy wykonać następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="ef802-235">**To assign Britta Simon to HR2day by Merces, take the following steps:**</span></span>

1. <span data-ttu-id="ef802-236">W portalu Azure Otwórz widok aplikacji, przejdź do widoku katalogu, a następnie przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="ef802-236">In the Azure portal, open the applications view, go to the directory view, and then go to **Enterprise applications**.</span></span> <span data-ttu-id="ef802-237">Następnie wybierz pozycję **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="ef802-237">Next, select **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="ef802-239">Na liście aplikacji zaznacz **HR2day przez Merces**.</span><span class="sxs-lookup"><span data-stu-id="ef802-239">In the applications list, select **HR2day by Merces**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. <span data-ttu-id="ef802-241">W menu po lewej stronie wybierz **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ef802-241">In the menu on the left, select **Users and groups**.</span></span>

    ![Przypisz użytkownika][202] 

4. <span data-ttu-id="ef802-243">Wybierz **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ef802-243">Select the **Add** button.</span></span> <span data-ttu-id="ef802-244">Następnie w **Dodaj przydziału** okno dialogowe, wybierz opcję **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="ef802-244">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Przypisz użytkownika][203]

5. <span data-ttu-id="ef802-246">W **użytkowników i grup** okna dialogowego, **użytkowników** listy, wybierz **Simona Britta**.</span><span class="sxs-lookup"><span data-stu-id="ef802-246">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="ef802-247">Kliknij przycisk **wybierz** przycisku.</span><span class="sxs-lookup"><span data-stu-id="ef802-247">Click the **Select** button.</span></span>

7. <span data-ttu-id="ef802-248">W **Dodaj przydziału** okno dialogowe, wybierz opcję **przypisać**.</span><span class="sxs-lookup"><span data-stu-id="ef802-248">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="ef802-249">Test rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="ef802-249">Test single sign-on</span></span>

<span data-ttu-id="ef802-250">Celem tej sekcji służy do testowania konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="ef802-250">The objective of this section is to test your Azure AD single sign-on configuration by using the Access Panel.</span></span>  

<span data-ttu-id="ef802-251">Po wybraniu HR2day przez Kafelek Merces w panelu dostępu, można automatycznie pobrać zalogowany HR2day Twojego przez aplikację Merces.</span><span class="sxs-lookup"><span data-stu-id="ef802-251">When you select the HR2day by Merces tile in the Access Panel, you automatically get signed in  to your HR2day by Merces application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ef802-252">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="ef802-252">Additional resources</span></span>

* [<span data-ttu-id="ef802-253">Lista samouczków dotyczących sposobu integracji aplikacji SaaS w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ef802-253">List of tutorials about how to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ef802-254">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ef802-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

