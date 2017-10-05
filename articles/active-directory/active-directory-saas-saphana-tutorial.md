---
title: 'Samouczek: Integracji Azure Active Directory z SAP HANA | Dokumentacja firmy Microsoft'
description: "Informacje o sposobie konfigurowania rejestracji jednokrotnej między usługą Azure Active Directory i SAP HANA."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: cef4a146-f4b0-4e94-82de-f5227a4b462c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: a7e73f6ee763d1005ad85935cf2d8f6b24ecf116
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-hana"></a><span data-ttu-id="1492c-103">Samouczek: Integracji Azure Active Directory z SAP HANA</span><span class="sxs-lookup"><span data-stu-id="1492c-103">Tutorial: Azure Active Directory integration with SAP HANA</span></span>

<span data-ttu-id="1492c-104">Z tego samouczka dowiesz się sposobu integracji z usługą Azure Active Directory (Azure AD) SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1492c-104">In this tutorial, you learn how to integrate SAP HANA with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1492c-105">Integrowanie SAP HANA z usługą Azure AD zapewnia następujące korzyści:</span><span class="sxs-lookup"><span data-stu-id="1492c-105">Integrating SAP HANA with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="1492c-106">Można kontrolować w usłudze Azure AD, który ma dostęp do programu SAP HANA</span><span class="sxs-lookup"><span data-stu-id="1492c-106">You can control in Azure AD who has access to SAP HANA</span></span>
- <span data-ttu-id="1492c-107">Umożliwia użytkownikom automatycznie pobrać zalogowane do SAP HANA (logowanie jednokrotne) z konta usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1492c-107">You can enable your users to automatically get signed-on to SAP HANA (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1492c-108">Możesz zarządzać kont w jednej centralnej lokalizacji - portalu Azure</span><span class="sxs-lookup"><span data-stu-id="1492c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="1492c-109">Jeśli chcesz dowiedzieć się więcej informacji o integracji aplikacji SaaS w usłudze Azure AD, zobacz [co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1492c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1492c-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="1492c-110">Prerequisites</span></span>

<span data-ttu-id="1492c-111">Aby skonfigurować integrację usługi Azure AD z SAP HANA, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="1492c-111">To configure Azure AD integration with SAP HANA, you need the following items:</span></span>

- <span data-ttu-id="1492c-112">Subskrypcję usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1492c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1492c-113">SAP HANA logowanie jednokrotne włączone subskrypcji</span><span class="sxs-lookup"><span data-stu-id="1492c-113">A SAP HANA single sign-on enabled subscription</span></span>
- <span data-ttu-id="1492c-114">HANA uruchomione wystąpienie na publicznych IaaS, lokalnymi, maszynach wirtualnych platformy Azure lub SAP dużych wystąpień na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="1492c-114">A running HANA Instance either on any public IaaS, on-premises, Azure VMs or SAP Large Instances in Azure</span></span>
- <span data-ttu-id="1492c-115">Interfejs sieci Web administracji XSA jak również zainstalowana w wystąpieniu HANA Studio HANA.</span><span class="sxs-lookup"><span data-stu-id="1492c-115">The XSA Administration Web Interface as well as HANA Studio installed on the HANA instance.</span></span>

> [!NOTE]
> <span data-ttu-id="1492c-116">Aby przetestować kroki opisane w tym samouczku, zaleca się używania środowiska produkcyjnego programu SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1492c-116">To test the steps in this tutorial, we do not recommend using a production environment of SAP HANA.</span></span> <span data-ttu-id="1492c-117">Przetestowanie integracji w rozwoju lub środowisko przejściowe aplikacji, a następnie użyj środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="1492c-117">Test the integration first in development or staging environment of the application and then use the production environment.</span></span>

<span data-ttu-id="1492c-118">Aby przetestować kroki opisane w tym samouczku, należy wykonać te zalecenia:</span><span class="sxs-lookup"><span data-stu-id="1492c-118">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1492c-119">Nie należy używać środowiska produkcyjnego, jeśli jest to konieczne.</span><span class="sxs-lookup"><span data-stu-id="1492c-119">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1492c-120">Jeśli nie masz środowisko wersji próbnej usługi Azure AD, możesz [uzyskać miesięczna wersja próbna](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1492c-120">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1492c-121">Opis scenariusza</span><span class="sxs-lookup"><span data-stu-id="1492c-121">Scenario description</span></span>
<span data-ttu-id="1492c-122">W tym samouczku można przetestować usługę Azure AD rejestracji jednokrotnej w środowisku testowym.</span><span class="sxs-lookup"><span data-stu-id="1492c-122">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1492c-123">Scenariusz opisany w tym samouczku składa się z dwóch głównych elementów:</span><span class="sxs-lookup"><span data-stu-id="1492c-123">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1492c-124">Dodawanie SAP HANA z galerii</span><span class="sxs-lookup"><span data-stu-id="1492c-124">Adding SAP HANA from the gallery</span></span>
2. <span data-ttu-id="1492c-125">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1492c-125">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-hana-from-the-gallery"></a><span data-ttu-id="1492c-126">Dodawanie SAP HANA z galerii</span><span class="sxs-lookup"><span data-stu-id="1492c-126">Adding SAP HANA from the gallery</span></span>
<span data-ttu-id="1492c-127">Aby skonfigurować integrację usługi Azure AD SAP HANA, należy dodać SAP HANA z galerii do listy zarządzanych aplikacji SaaS.</span><span class="sxs-lookup"><span data-stu-id="1492c-127">To configure the integration of SAP HANA into Azure AD, you need to add SAP HANA from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="1492c-128">**Aby dodać SAP HANA z galerii, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1492c-128">**To add SAP HANA from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="1492c-129">W  **[portalu Azure](https://portal.azure.com)**, na panelu nawigacyjnym po lewej stronie kliknij **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1492c-129">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Przycisk usługi Azure Active Directory][1]

2. <span data-ttu-id="1492c-131">Przejdź do **aplikacje dla przedsiębiorstw**.</span><span class="sxs-lookup"><span data-stu-id="1492c-131">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="1492c-132">Następnie przejdź do **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1492c-132">Then go to **All applications**.</span></span>

    ![Blok aplikacje przedsiębiorstwa][2]
    
3. <span data-ttu-id="1492c-134">Aby dodać nową aplikację, kliknij przycisk **nowej aplikacji** przycisk w górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1492c-134">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Nowy przycisk aplikacji][3]

4. <span data-ttu-id="1492c-136">W polu wyszukiwania wpisz **SAP HANA**, wybierz pozycję **SAP HANA** z panelu wyników kliknięcie **Dodaj** przycisk, aby dodać aplikację.</span><span class="sxs-lookup"><span data-stu-id="1492c-136">In the search box, type **SAP HANA**, select **SAP HANA** from result panel then click **Add** button to add the application.</span></span> 

    ![Nowa aplikacja](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1492c-138">Konfigurowanie i testowanie usługi Azure AD logowanie jednokrotne</span><span class="sxs-lookup"><span data-stu-id="1492c-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1492c-139">W tej sekcji możesz skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SAP HANA oparte na koncie użytkownika testu o nazwie "Britta Simona".</span><span class="sxs-lookup"><span data-stu-id="1492c-139">In this section, you configure and test Azure AD single sign-on with SAP HANA based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="1492c-140">Dla rejestracji jednokrotnej do pracy usługi Azure AD musi wiedzieć, użytkownik odpowiednika w SAP HANA jest dla użytkownika, w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1492c-140">For single sign-on to work, Azure AD needs to know what the counterpart user in SAP HANA is to a user in Azure AD.</span></span> <span data-ttu-id="1492c-141">Innymi słowy musi można ustanowić łącze relację między użytkownikiem usługi Azure AD i danemu użytkownikowi w SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1492c-141">In other words, a link relationship between an Azure AD user and the related user in SAP HANA needs to be established.</span></span>

<span data-ttu-id="1492c-142">SAP HANA przypisywanie wartości **nazwy użytkownika** w usłudze Azure AD jako wartość **Username** do ustanawiania relacji łącza.</span><span class="sxs-lookup"><span data-stu-id="1492c-142">In SAP HANA, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="1492c-143">Aby skonfigurować i przetestować usługi Azure AD rejestracji jednokrotnej z SAP HANA, należy wykonać poniższe bloki konstrukcyjne:</span><span class="sxs-lookup"><span data-stu-id="1492c-143">To configure and test Azure AD single sign-on with SAP HANA, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="1492c-144">**[Konfigurowanie usługi Azure AD rejestracji jednokrotnej](#configuring-azure-ad-single-sign-on)**  — aby umożliwić użytkownikom korzystać z tej funkcji.</span><span class="sxs-lookup"><span data-stu-id="1492c-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="1492c-145">**[Tworzenie użytkownika testowego usługi Azure AD](#creating-an-azure-ad-test-user)**  — do przetestowania usługi Azure AD rejestracji jednokrotnej z Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1492c-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1492c-146">**[Tworzenie użytkownika testowego SAP HANA](#creating-a-sap-hana-test-user)**  — w celu zapewnienia odpowiednikiem Simona Britta SAP HANA, połączonej z usługi Azure AD reprezentację użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1492c-146">**[Creating a SAP HANA test user](#creating-a-sap-hana-test-user)** - to have a counterpart of Britta Simon in SAP HANA that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="1492c-147">**[Przypisanie użytkownika testowego usługi Azure AD](#assigning-the-azure-ad-test-user)**  — aby umożliwić Simona Britta do użycia usługi Azure AD rejestracji jednokrotnej.</span><span class="sxs-lookup"><span data-stu-id="1492c-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1492c-148">**[Testowanie rejestracji jednokrotnej](#testing-single-sign-on)**  — Aby sprawdzić, czy konfiguracja działa.</span><span class="sxs-lookup"><span data-stu-id="1492c-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1492c-149">Konfigurowanie usługi Azure AD rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1492c-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1492c-150">W tej sekcji można włączyć usługi Azure AD rejestracji jednokrotnej w portalu Azure i skonfigurować logowanie jednokrotne do aplikacji SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1492c-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAP HANA application.</span></span>

<span data-ttu-id="1492c-151">**Aby skonfigurować usługi Azure AD rejestracji jednokrotnej z SAP HANA, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1492c-151">**To configure Azure AD single sign-on with SAP HANA, perform the following steps:**</span></span>

1. <span data-ttu-id="1492c-152">W portalu Azure na **SAP HANA** strona integracji aplikacji, kliknij przycisk **logowanie jednokrotne**.</span><span class="sxs-lookup"><span data-stu-id="1492c-152">In the Azure portal, on the **SAP HANA** application integration page, click **Single sign-on**.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej][4]

2. <span data-ttu-id="1492c-154">Na **logowanie jednokrotne** okno dialogowe, wybierz opcję **tryb** jako **na języku SAML logowania jednokrotnego** Aby włączyć logowanie jednokrotne.</span><span class="sxs-lookup"><span data-stu-id="1492c-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Okno dialogowe rejestracji jednokrotnej](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_samlbase.png)

3. <span data-ttu-id="1492c-156">Na **adresy URL i SAP HANA domeny** sekcji, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1492c-156">On the **SAP HANA Domain and URLs** section, perform the following steps:</span></span>

    ![Domena i adres URL z jednym informacje logowania jednokrotnego](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_url.png)

    <span data-ttu-id="1492c-158">a.</span><span class="sxs-lookup"><span data-stu-id="1492c-158">a.</span></span> <span data-ttu-id="1492c-159">W **identyfikator** pole tekstowe, typu co:`HA100`</span><span class="sxs-lookup"><span data-stu-id="1492c-159">In the **Identifier** textbox, type as: `HA100`</span></span> 

    <span data-ttu-id="1492c-160">b.</span><span class="sxs-lookup"><span data-stu-id="1492c-160">b.</span></span> <span data-ttu-id="1492c-161">W **adres URL odpowiedzi** tekstowym, wpisz adres URL, używając następującego wzorca:`https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span><span class="sxs-lookup"><span data-stu-id="1492c-161">In the **Reply URL** textbox, type a URL using the following pattern: `https://<Customer-SAP-instance-url>/sap/hana/xs/saml/login.xscfunc`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1492c-162">Wartości te nie są prawdziwe.</span><span class="sxs-lookup"><span data-stu-id="1492c-162">These values are not real.</span></span> <span data-ttu-id="1492c-163">Rzeczywisty identyfikator i adres URL odpowiedzi, należy zaktualizować te wartości.</span><span class="sxs-lookup"><span data-stu-id="1492c-163">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="1492c-164">Skontaktuj się z [zespołem pomocy technicznej SAP HANA klienta](https://cloudplatform.sap.com/contact.html) uzyskać te wartości.</span><span class="sxs-lookup"><span data-stu-id="1492c-164">Contact [SAP HANA Client support team](https://cloudplatform.sap.com/contact.html) to get these values.</span></span> 

4. <span data-ttu-id="1492c-165">Na **certyfikat podpisywania SAML** kliknij **XML metadanych** , a następnie zapisz plik metadanych na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="1492c-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Łącze pobierania certyfikatu](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_certificate.png) 

    >[!Note]
    ><span data-ttu-id="1492c-167">Jeśli certyfikat nie jest aktywne następnie uaktywnić go, klikając pole wyboru "Uaktywnij nowy certyfikat" w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1492c-167">If certificate is not active then make it active by clicking the “Make new certificate active” checkbox in the Azure AD.</span></span> 

5. <span data-ttu-id="1492c-168">Aplikacja SAP HANA oczekuje potwierdzenia języka SAML w określonym formacie.</span><span class="sxs-lookup"><span data-stu-id="1492c-168">SAP HANA application expects the SAML assertions in a specific format.</span></span> <span data-ttu-id="1492c-169">Poniższy zrzut ekranu przedstawia przykład tego.</span><span class="sxs-lookup"><span data-stu-id="1492c-169">The following screenshot shows an example for this.</span></span> <span data-ttu-id="1492c-170">W tym miejscu możemy zamapowaniu **identyfikator użytkownika** z **ExtractMailPrefix()** funkcji **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="1492c-170">Here we have mapped the **User Identifier** with **ExtractMailPrefix()** function of **user.mail**.</span></span> <span data-ttu-id="1492c-171">Dzięki temu wartość prefiksu adres e-mail użytkownika, który jest unikatowy identyfikator użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1492c-171">This gives the prefix value of email of the user which is the unique User ID.</span></span> <span data-ttu-id="1492c-172">To są wysyłane do aplikacji SAP HANA w każdym pomyślnym odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="1492c-172">This is sent to the SAP HANA application in every successful response.</span></span>

    ![Konfigurowanie rejestracji jednokrotnej](./media/active-directory-saas-saphana-tutorial/attribute.png)

6. <span data-ttu-id="1492c-174">W **atrybuty użytkownika** sekcji na **logowanie jednokrotne** okna dialogowego:</span><span class="sxs-lookup"><span data-stu-id="1492c-174">In the **User Attributes** section on the **Single sign-on** dialog:</span></span>

    <span data-ttu-id="1492c-175">a.</span><span class="sxs-lookup"><span data-stu-id="1492c-175">a.</span></span> <span data-ttu-id="1492c-176">W **identyfikator użytkownika** listy rozwijanej wybierz **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="1492c-176">In the **User Identifier** dropdown list, select **ExtractMailPrefix**.</span></span>
    
    <span data-ttu-id="1492c-177">b.</span><span class="sxs-lookup"><span data-stu-id="1492c-177">b.</span></span> <span data-ttu-id="1492c-178">W **poczty** listy rozwijanej wybierz **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="1492c-178">In the **Mail** dropdown list, select **user.mail**.</span></span>

7. <span data-ttu-id="1492c-179">Kliknij przycisk **zapisać** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1492c-179">Click **Save** button.</span></span>

    ![Skonfiguruj przycisk pojedynczego logowania jednokrotnego Zapisz](./media/active-directory-saas-saphana-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="1492c-181">Do konfigurowania rejestracji jednokrotnej na **SAP HANA** strona, zaloguj się do sieci **konsoli sieci Web XSA HANA** przechodząc do odpowiednich końcowego HTTPS.</span><span class="sxs-lookup"><span data-stu-id="1492c-181">To configure single sign-on on **SAP HANA** side, login to your **HANA XSA Web Console**  by browsing to the respective HTTPS-endpoint.</span></span>

    > [!Note]
    > <span data-ttu-id="1492c-182">W domyślnej konfiguracji adres URL przekierowuje żądanie do strony logowania, co wymaga poświadczeń uwierzytelnionego użytkownika bazy danych SAP HANA do ukończenia procesu logowania.</span><span class="sxs-lookup"><span data-stu-id="1492c-182">In the default configuration, the URL redirects the request to a logon screen, which requires the credentials of an authenticated SAP HANA database user to complete the logon process.</span></span> <span data-ttu-id="1492c-183">Użytkownik, który loguje się musi mieć uprawnienia wymagane do wykonywania zadań administracyjnych SAML.</span><span class="sxs-lookup"><span data-stu-id="1492c-183">The user who logs on must have the privileges required to perform SAML administration tasks.</span></span>

9. <span data-ttu-id="1492c-184">W interfejsie sieci Web XSA, przejdź do **dostawca tożsamości SAML** i z tego miejsca, kliknij przycisk **"+"** — przycisk w dolnej części ekranu, aby wyświetlić okienko dodać informacje dostawcy tożsamości i wykonaj następujące czynności kroki:</span><span class="sxs-lookup"><span data-stu-id="1492c-184">In the XSA Web Interface, navigate to **SAML Identity Provider** and from there, click the **“+”** -button on the bottom of the screen to display the Add Identity Provider Info pane and perform the following steps:</span></span>

    ![Dodaj dostawcę tożsamości](./media/active-directory-saas-saphana-tutorial/sap1.png)

    <span data-ttu-id="1492c-186">a.</span><span class="sxs-lookup"><span data-stu-id="1492c-186">a.</span></span> <span data-ttu-id="1492c-187">W **dodać informacje dostawcy tożsamości** okienku Wklej zawartość XML metadanych, który został pobrany z portalu Azure do **metadanych** pola tekstowego.</span><span class="sxs-lookup"><span data-stu-id="1492c-187">In the **Add Identity Provider Info** pane, paste the contents of the Metadata XML, which you have downloaded from Azure portal into the **Metadata** textbox.</span></span>

    ![Dodaj ustawienia dostawcy tożsamości](./media/active-directory-saas-saphana-tutorial/sap2.png)

    <span data-ttu-id="1492c-189">b.</span><span class="sxs-lookup"><span data-stu-id="1492c-189">b.</span></span> <span data-ttu-id="1492c-190">Jeśli zawartość dokumentu XML są prawidłowe, proces analizowania wyodrębnia informacje wymagane do wstawienia do **podmiotu, identyfikator jednostki i wystawcy** pola w obszarze ekranu ogólne danych i pola Adres URL na ekranie docelowego obszar, na przykład  **podstawowego adresu URL i adresu URL SingleSignOn (*)**.</span><span class="sxs-lookup"><span data-stu-id="1492c-190">If the contents of the XML document are valid, the parsing process extracts the information required to insert into the **Subject, Entity ID, and Issuer** fields in the General Data screen area, and the URL fields in the Destination screen area, for example, **Base URL and SingleSignOn URL (*)**.</span></span>

    ![Dodaj ustawienia dostawcy tożsamości](./media/active-directory-saas-saphana-tutorial/sap3.png)

    <span data-ttu-id="1492c-192">c.</span><span class="sxs-lookup"><span data-stu-id="1492c-192">c.</span></span> <span data-ttu-id="1492c-193">W polu Nazwa obszaru danych ogólne ekranu wprowadź nazwę dla nowego logowania jednokrotnego SAML dostawcy tożsamości.</span><span class="sxs-lookup"><span data-stu-id="1492c-193">In the Name box of the General Data screen area, enter a name for the new SAML SSO identity provider.</span></span>

    > [!Note]
    > <span data-ttu-id="1492c-194">Nazwa SAML IDP jest wymagana i musi być unikatowa. wygląda na to, na liście dostępnych IDPs SAML, która jest wyświetlana, wtedy, gdy metoda uwierzytelniania SAP HANA XS do użycia przez aplikacje, na przykład w obszarze uwierzytelnianie ekranu narzędzia do administrowania artefaktu XS SAML.</span><span class="sxs-lookup"><span data-stu-id="1492c-194">The name of the SAML IDP is mandatory and must be unique; it appears in the list of available SAML IDPs that is displayed, if you select SAML as the authentication method for SAP HANA XS applications to use, for example, in the Authentication screen area of the XS Artifact Administration tool.</span></span>

10. <span data-ttu-id="1492c-195">Zapisz szczegóły nowego dostawcy tożsamości SAML.</span><span class="sxs-lookup"><span data-stu-id="1492c-195">Save the details of the new SAML identity provider.</span></span> <span data-ttu-id="1492c-196">Wybierz **zapisać** zapisać szczegóły dostawca tożsamości SAML i dodać nowe IDP SAML do listy znanych IDPs SAML.</span><span class="sxs-lookup"><span data-stu-id="1492c-196">Choose **Save** to save the details of the SAML identity provider and add the new SAML IDP to the list of known SAML IDPs.</span></span>

    ![Przyciskiem Zapisz](./media/active-directory-saas-saphana-tutorial/sap4.png)

11. <span data-ttu-id="1492c-198">W Studio HANA w ramach właściwości systemu **konfiguracji** karcie, po prostu filtrowania ustawień przez **saml** i dostosować **assertion_timeout** z **10 s**  do **120 s**.</span><span class="sxs-lookup"><span data-stu-id="1492c-198">In HANA Studio within the system properties of the **Configuration** tab, just filter settings by **saml** and adjust the **assertion_timeout** from **10 sec** to **120 sec**.</span></span>

    ![Ustawienie assertion_timeout](./media/active-directory-saas-saphana-tutorial/sap7.png)

> [!TIP]
> <span data-ttu-id="1492c-200">Teraz możesz przeczytać zwięzły wersji tych instrukcji wewnątrz [portalu Azure](https://portal.azure.com), podczas konfigurowania aplikacji!</span><span class="sxs-lookup"><span data-stu-id="1492c-200">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="1492c-201">Po dodaniu tej aplikacji z **usługi Active Directory > aplikacje dla przedsiębiorstw** po prostu kliknij **rejestracji jednokrotnej** karcie i dostęp do dokumentacji osadzonych za pomocą **konfiguracji** sekcji u dołu.</span><span class="sxs-lookup"><span data-stu-id="1492c-201">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="1492c-202">Więcej o funkcji dokumentacji osadzonego w tym miejscu: [dokumentacji osadzonych usługi Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1492c-202">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1492c-203">Tworzenie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1492c-203">Creating an Azure AD test user</span></span>
<span data-ttu-id="1492c-204">Celem tej sekcji jest tworzenie użytkownika testowego w portalu Azure o nazwie Simona Britta.</span><span class="sxs-lookup"><span data-stu-id="1492c-204">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Tworzenie użytkowników usługi Azure AD][100]

<span data-ttu-id="1492c-206">**Aby utworzyć użytkownika testowego w usłudze Azure AD, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1492c-206">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="1492c-207">W **portalu Azure**, w lewym okienku nawigacji, kliknij polecenie **usługi Azure Active Directory** ikony.</span><span class="sxs-lookup"><span data-stu-id="1492c-207">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Przycisk usługi Azure Active Directory](./media/active-directory-saas-saphana-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1492c-209">Aby wyświetlić listę użytkowników, przejdź do **użytkowników i grup** i kliknij przycisk **wszyscy użytkownicy**.</span><span class="sxs-lookup"><span data-stu-id="1492c-209">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !["Użytkownicy i grupy" i "Wszyscy użytkownicy" łącza](./media/active-directory-saas-saphana-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1492c-211">Aby otworzyć **użytkownika** okna dialogowego, kliknij przycisk **Dodaj** górnej części okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1492c-211">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Przycisk Dodaj](./media/active-directory-saas-saphana-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1492c-213">Na **użytkownika** okna dialogowego strony, należy wykonać następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1492c-213">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Okno dialogowe użytkownika](./media/active-directory-saas-saphana-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1492c-215">a.</span><span class="sxs-lookup"><span data-stu-id="1492c-215">a.</span></span> <span data-ttu-id="1492c-216">W **nazwa** pole tekstowe, typ **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1492c-216">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1492c-217">b.</span><span class="sxs-lookup"><span data-stu-id="1492c-217">b.</span></span> <span data-ttu-id="1492c-218">W **nazwy użytkownika** pole tekstowe, typ **adres e-mail** z BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1492c-218">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1492c-219">c.</span><span class="sxs-lookup"><span data-stu-id="1492c-219">c.</span></span> <span data-ttu-id="1492c-220">Wybierz **Pokaż hasło** i zanotuj wartość **hasło**.</span><span class="sxs-lookup"><span data-stu-id="1492c-220">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="1492c-221">d.</span><span class="sxs-lookup"><span data-stu-id="1492c-221">d.</span></span> <span data-ttu-id="1492c-222">Kliknij przycisk **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="1492c-222">Click **Create**.</span></span>
 
### <a name="creating-a-sap-hana-test-user"></a><span data-ttu-id="1492c-223">Tworzenie użytkownika testowego SAP HANA</span><span class="sxs-lookup"><span data-stu-id="1492c-223">Creating a SAP HANA test user</span></span>

<span data-ttu-id="1492c-224">Aby umożliwić użytkownikom usługi Azure AD zalogować się do programu SAP HANA, muszą mieć przydzielone do programu SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1492c-224">To enable Azure AD users to log in to SAP HANA, they must be provisioned into SAP HANA.</span></span>
<span data-ttu-id="1492c-225">SAP HANA obsługę w czasie, który jest domyślnie włączone.</span><span class="sxs-lookup"><span data-stu-id="1492c-225">SAP HANA supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="1492c-226">Jeśli trzeba ręcznie utworzyć użytkownika, wykonaj następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1492c-226">If you need to create a user manually, perform the following steps:</span></span>

>[!Note]
><span data-ttu-id="1492c-227">Uwierzytelnianie zewnętrzne używane przez użytkownika, można zmienić.</span><span class="sxs-lookup"><span data-stu-id="1492c-227">You can change the external authentication used by the user.</span></span>
<span data-ttu-id="1492c-228">Użytkownicy zewnętrzni są uwierzytelniani, za pomocą zewnętrznego systemu, na przykład system protokołu Kerberos.</span><span class="sxs-lookup"><span data-stu-id="1492c-228">External users are authenticated using an external system, for example a Kerberos system.</span></span> <span data-ttu-id="1492c-229">Aby uzyskać szczegółowe informacje o tożsamości zewnętrznych, skontaktuj się z [administrator domeny](https://cloudplatform.sap.com/contact.html).</span><span class="sxs-lookup"><span data-stu-id="1492c-229">For detailed information about external identities, contact your [domain administrator](https://cloudplatform.sap.com/contact.html).</span></span>

1. <span data-ttu-id="1492c-230">Otwórz [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) jako administrator i Włącz użytkownika bazy danych dla logowania jednokrotnego SAML.</span><span class="sxs-lookup"><span data-stu-id="1492c-230">Open the [SAP HANA Studio](https://help.sap.com/viewer/a2a49126a5c546a9864aae22c05c3d0e/2.0.01/en-us) as an administrator and enable the DB-User for SAML SSO.</span></span>

    ![Utwórz użytkownika](./media/active-directory-saas-saphana-tutorial/sap5.png)

2. <span data-ttu-id="1492c-232">Znaczników niewidoczne pola wyboru po lewej **SAML** i kliknij link Konfiguruj.</span><span class="sxs-lookup"><span data-stu-id="1492c-232">Tick the invisible checkbox to the left of **SAML** and follow the Configure link.</span></span>

3. <span data-ttu-id="1492c-233">Kliknij przycisk **Dodaj** dodany SAML IDP i kliknij przycisk **OK** wybranie odpowiednich IDP SAML.</span><span class="sxs-lookup"><span data-stu-id="1492c-233">Click **Add** to add the SAML IDP and click **OK** selecting the appropriate SAML IDP.</span></span>

4. <span data-ttu-id="1492c-234">Dodaj **tożsamości zewnętrznych** (np.</span><span class="sxs-lookup"><span data-stu-id="1492c-234">Add the **External Identity** (ex.</span></span> <span data-ttu-id="1492c-235">W tym miejscu BrittaSimon) lub wybierz **"Wszystkie"** i kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="1492c-235">BrittaSimon here) or choose **"Any"** and click **OK**.</span></span>

    >[!Note]
    ><span data-ttu-id="1492c-236">Jeśli nie zaznaczono pole "Wszystkie", a następnie nazwę użytkownika w HANA musi dokładnie odpowiadać nazwie użytkownika w głównej nazwy użytkownika przed sufiksem domeny (np. BrittaSimon@contoso.com staje się BrittaSimon w HANA).</span><span class="sxs-lookup"><span data-stu-id="1492c-236">If "ANY" check-box is not checked, then the user name in HANA needs to exactly match the name of the user in the UPN before the domain suffix (i.e. BrittaSimon@contoso.com would become BrittaSimon in HANA).</span></span>

5. <span data-ttu-id="1492c-237">Do celów testowych, przypisać wszystkie **"XS"** ról do użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1492c-237">For testing purposes, assign all **"XS"** roles to the user.</span></span>

    ![Przypisywanie ról](./media/active-directory-saas-saphana-tutorial/sap6.png)

    > [!TIP]
    > <span data-ttu-id="1492c-239">Należy podać te uprawnienia, które są odpowiednie dla Twojej przypadki użycia tylko.</span><span class="sxs-lookup"><span data-stu-id="1492c-239">You should give those permissions appropriate for your use cases, only.</span></span>

6. <span data-ttu-id="1492c-240">Zapisz użytkownika.</span><span class="sxs-lookup"><span data-stu-id="1492c-240">Save the user.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="1492c-241">Przypisanie użytkownika testowego usługi Azure AD</span><span class="sxs-lookup"><span data-stu-id="1492c-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="1492c-242">W tej sekcji można włączyć Simona Britta do używania Azure logowania jednokrotnego za udzielanie dostępu do programu SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1492c-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAP HANA.</span></span>

![Przypisanie roli użytkownika][200] 

<span data-ttu-id="1492c-244">**Aby przypisać Simona Britta SAP HANA, wykonaj następujące czynności:**</span><span class="sxs-lookup"><span data-stu-id="1492c-244">**To assign Britta Simon to SAP HANA, perform the following steps:**</span></span>

1. <span data-ttu-id="1492c-245">W portalu Azure Otwórz widok aplikacji, a następnie przejdź do widoku katalogu i przejdź do **aplikacje dla przedsiębiorstw** kliknięcie **wszystkie aplikacje**.</span><span class="sxs-lookup"><span data-stu-id="1492c-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Przypisz użytkownika][201] 

2. <span data-ttu-id="1492c-247">Na liście aplikacji zaznacz **SAP HANA**.</span><span class="sxs-lookup"><span data-stu-id="1492c-247">In the applications list, select **SAP HANA**.</span></span>

    ![Przypisz użytkownika](./media/active-directory-saas-saphana-tutorial/tutorial_saphana_app.png) 

3. <span data-ttu-id="1492c-249">W menu po lewej stronie kliknij **użytkowników i grup**.</span><span class="sxs-lookup"><span data-stu-id="1492c-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Łącze "Użytkownicy i grupy"][202] 

4. <span data-ttu-id="1492c-251">Kliknij przycisk **Dodaj** przycisku.</span><span class="sxs-lookup"><span data-stu-id="1492c-251">Click **Add** button.</span></span> <span data-ttu-id="1492c-252">Następnie wybierz **użytkowników i grup** na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1492c-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![W okienku Dodaj przydziału][203]

5. <span data-ttu-id="1492c-254">Na **użytkowników i grup** okno dialogowe, wybierz opcję **Simona Britta** na liście Użytkownicy.</span><span class="sxs-lookup"><span data-stu-id="1492c-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="1492c-255">Kliknij przycisk **wybierz** znajdującego się na **użytkowników i grup** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1492c-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1492c-256">Kliknij przycisk **przypisać** znajdującego się na **Dodaj przydziału** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="1492c-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1492c-257">Testowanie rejestracji jednokrotnej</span><span class="sxs-lookup"><span data-stu-id="1492c-257">Testing single sign-on</span></span>

<span data-ttu-id="1492c-258">W tej sekcji można przetestować konfiguracji usługi Azure AD pojedynczego logowania za pomocą panelu dostępu.</span><span class="sxs-lookup"><span data-stu-id="1492c-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="1492c-259">Po kliknięciu kafelka SAP HANA w panelu dostępu użytkownik powinien pobrać automatycznie zalogowane do aplikacji SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="1492c-259">When you click the SAP HANA tile in the Access Panel, you should get automatically signed-on to your SAP HANA application.</span></span>
<span data-ttu-id="1492c-260">Aby uzyskać więcej informacji na temat panelu dostępu, zobacz [wprowadzenie do panelu dostępu](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1492c-260">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1492c-261">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="1492c-261">Additional resources</span></span>

* [<span data-ttu-id="1492c-262">Lista samouczków dotyczących sposobów integracji aplikacji SaaS przy użyciu usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1492c-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1492c-263">Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1492c-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-saphana-tutorial/tutorial_general_203.png

