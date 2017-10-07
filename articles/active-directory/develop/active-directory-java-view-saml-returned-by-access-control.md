---
title: "aaaView zwrócił SAML hello usłudze kontroli dostępu (Java)"
description: "Dowiedz się, jak tooview SAML zwrócony przez hello usłudze kontroli dostępu w aplikacji Java hostowanej na platformie Azure."
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6cd216f9-eb43-46b4-b30d-f194d0ae2d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.custom: aaddev
ms.openlocfilehash: b6733bc98b505cfa89a4ce456f368ee15da11427
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-saml-returned-by-hello-azure-access-control-service"></a><span data-ttu-id="eaf81-103">Jak tooview SAML zwrócony przez hello usłudze kontroli dostępu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="eaf81-103">How tooview SAML returned by hello Azure Access Control Service</span></span>
<span data-ttu-id="eaf81-104">W tym przewodniku opisano sposób hello tooview bazowy Security (Assertion Markup Language SAML) wypychaniu tooyour aplikacji hello Azure usługi kontroli dostępu (ACS).</span><span class="sxs-lookup"><span data-stu-id="eaf81-104">This guide will show you how tooview hello underlying Security Assertion Markup Language (SAML) returned tooyour application by hello Azure Access Control Service (ACS).</span></span> <span data-ttu-id="eaf81-105">Przewodnik Hello opiera się na powitania [jak tooAuthenticate sieci Web użytkownikom Eclipse przy użyciu usługi kontroli dostępu platformy Azure](active-directory-java-authenticate-users-access-control-eclipse.md) tematu, podając kod, który wyświetla informacje o hello SAML.</span><span class="sxs-lookup"><span data-stu-id="eaf81-105">hello guide builds on hello [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) topic, by providing code that displays hello SAML information.</span></span> <span data-ttu-id="eaf81-106">aplikacji Hello ukończone będzie wyglądać podobnie następujące toohello.</span><span class="sxs-lookup"><span data-stu-id="eaf81-106">hello completed application will look similar toohello following.</span></span>

![Przykładowe dane wyjściowe SAML][saml_output]

<span data-ttu-id="eaf81-108">Aby uzyskać więcej informacji dotyczących usług ACS, zobacz hello [następne kroki](#next_steps) sekcji.</span><span class="sxs-lookup"><span data-stu-id="eaf81-108">For more information on ACS, see hello [Next steps](#next_steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="eaf81-109">Hello Azure dostęp do usług formant filtru jest podgląd technologii społeczności.</span><span class="sxs-lookup"><span data-stu-id="eaf81-109">hello Azure Access Services Control Filter is a community technology preview.</span></span> <span data-ttu-id="eaf81-110">Jako wydaniu wstępnym oprogramowania go nie jest oficjalnie obsługiwana przez firmę Microsoft.</span><span class="sxs-lookup"><span data-stu-id="eaf81-110">As pre-release software, it is not formally supported by Microsoft.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="eaf81-111">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eaf81-111">Prerequisites</span></span>
<span data-ttu-id="eaf81-112">toocomplete hello zadania w tym przewodniku, pełną hello próbki w [jak tooAuthenticate sieci Web użytkownikom Eclipse przy użyciu usługi kontroli dostępu platformy Azure](active-directory-java-authenticate-users-access-control-eclipse.md) i używać go jako hello punkt początkowy dla tego samouczka.</span><span class="sxs-lookup"><span data-stu-id="eaf81-112">toocomplete hello tasks in this guide, complete hello sample at [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) and use it as hello starting point for this tutorial.</span></span>

## <a name="add-hello-jspwriter-library-tooyour-build-path-and-deployment-assembly"></a><span data-ttu-id="eaf81-113">Dodaj hello JspWriter biblioteki tooyour kompilacji ścieżkę i wdrożenia zestawu</span><span class="sxs-lookup"><span data-stu-id="eaf81-113">Add hello JspWriter library tooyour build path and deployment assembly</span></span>
<span data-ttu-id="eaf81-114">Dodaj bibliotekę hello, który zawiera hello **javax.servlet.jsp.JspWriter** tooyour klasy kompilacji zestawu ścieżkę i wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="eaf81-114">Add hello library that contains hello **javax.servlet.jsp.JspWriter** class tooyour build path and deployment assembly.</span></span> <span data-ttu-id="eaf81-115">Jeśli używasz Tomcat Biblioteka hello jest **jsp api.jar**, który znajduje się w hello Apache **lib** folderu.</span><span class="sxs-lookup"><span data-stu-id="eaf81-115">If you are using Tomcat, hello library is **jsp-api.jar**, which is located in hello Apache **lib** folder.</span></span>

1. <span data-ttu-id="eaf81-116">W obszarze Eksplorator projektów w środowisku Eclipse, kliknij prawym przyciskiem myszy **MyACSHelloWorld**, kliknij przycisk **ścieżkę kompilacji**, kliknij przycisk **Konfiguruj ścieżkę kompilacji**, kliknij hello **biblioteki** , a następnie kliknij pozycję **Dodaj zewnętrzne JARs**.</span><span class="sxs-lookup"><span data-stu-id="eaf81-116">In Eclipse's Project Explorer, right-click **MyACSHelloWorld**, click **Build Path**, click **Configure Build Path**, click hello **Libraries** tab, and then click **Add External JARs**.</span></span>
2. <span data-ttu-id="eaf81-117">W hello **JAR wybór** okno dialogowe, przejdź toohello niezbędne JAR, zaznacz go, a następnie kliknij **Otwórz**.</span><span class="sxs-lookup"><span data-stu-id="eaf81-117">In hello **JAR Selection** dialog, navigate toohello necessary JAR, select it, and then click **Open**.</span></span>
3. <span data-ttu-id="eaf81-118">Z hello **właściwości MyACSHelloWorld** nadal otwarty, kliknij przycisk okna dialogowego **wdrożenia zestawu**.</span><span class="sxs-lookup"><span data-stu-id="eaf81-118">With hello **Properties for MyACSHelloWorld** dialog still open, click **Deployment Assembly**.</span></span>
4. <span data-ttu-id="eaf81-119">W hello **zestawu wdrażania Web** okna dialogowego, kliknij przycisk **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="eaf81-119">In hello **Web Deployment Assembly** dialog, click **Add**.</span></span>
5. <span data-ttu-id="eaf81-120">W hello **nowe dyrektywa zestawu** okna dialogowego, kliknij przycisk **wpisy ścieżka kompilacji języka Java** , a następnie kliknij przycisk **dalej**.</span><span class="sxs-lookup"><span data-stu-id="eaf81-120">In hello **New Assembly Directive** dialog, click **Java Build Path Entries** and then click **Next**.</span></span>
6. <span data-ttu-id="eaf81-121">Wybierz odpowiednią bibliotekę hello i kliknij przycisk **Zakończ**.</span><span class="sxs-lookup"><span data-stu-id="eaf81-121">Select hello appropriate library and click **Finish**.</span></span>
7. <span data-ttu-id="eaf81-122">Kliknij przycisk **OK** tooclose hello **właściwości MyACSHelloWorld** okna dialogowego.</span><span class="sxs-lookup"><span data-stu-id="eaf81-122">Click **OK** tooclose hello **Properties for MyACSHelloWorld** dialog.</span></span>

## <a name="modify-hello-jsp-file-toodisplay-saml"></a><span data-ttu-id="eaf81-123">Modyfikowanie toodisplay pliku JSP hello SAML</span><span class="sxs-lookup"><span data-stu-id="eaf81-123">Modify hello JSP file toodisplay SAML</span></span>
<span data-ttu-id="eaf81-124">Modyfikowanie **index.jsp** hello toouse następującego kodu.</span><span class="sxs-lookup"><span data-stu-id="eaf81-124">Modify **index.jsp** toouse hello following code.</span></span>

    <%@ page language="java" contentType="text/html; charset=UTF-8"
        pageEncoding="UTF-8"%>
        <%@ page import="javax.xml.parsers.*"
                 import="javax.xml.transform.*"
                 import="org.w3c.dom.*"
                 import="java.io.*"
                 import="javax.xml.transform.stream.*"
                 import="javax.xml.transform.dom.*"
                 import="javax.xml.xpath.*"
                 import="javax.servlet.jsp.JspWriter" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Sample ACS Filter</title>
    </head>
    <body>
        <h3>SAML information from sample ACS program</h3>
        <%!
        void displaySAMLInfo(Node node, String parent, JspWriter out)
        {

            try
            {
                String nodeName;
                int nChild, i;

                nodeName = node.getNodeName();
                out.println("<br>");
                out.println("<u>Examining <b>" + parent + nodeName + "</b></u><br>");

                   // Attributes.
                   NamedNodeMap attribsMap = node.getAttributes();
                   if (null != attribsMap)
                   {
                         for (i=0; i < attribsMap.getLength(); i++)
                         {
                                Node attrib = attribsMap.item(i);
                                out.println("Attribute: <b>" + attrib.getNodeName() + "</b>: " + attrib.getNodeValue()  + "<br>");
                         }
                   }

                   // Child nodes.
                   NodeList list = node.getChildNodes();
                   if (null != list)
                    {
                          nChild = list.getLength();
                          if (nChild > 0)
                          {                    

                                 // If it is a text node, just print hello text.
                                 if (list.item(0).getNodeName() == "#text")
                                 {
                                     out.println("Text value: <b>" + list.item(0).getTextContent() + "</b><br>");
                                 }
                                 else
                                 {
                                     // Print out hello child node names.
                                     out.print("Contains " + nChild + " child node(s): ");   
                                        for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);

                                        out.print("<b>" + temp.getNodeName() + "</b>");
                                        if (i < nChild - 1)
                                        {
                                            // Separate hello names.
                                            out.print(", ");
                                        }
                                        else
                                        {
                                            // Finish hello sentence.
                                            out.print(".");
                                        }

                                     }
                                     out.println("<br>");

                                     // Process hello child nodes.
                                     for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);
                                        displaySAMLInfo(temp, parent + nodeName + "\\", out);
                                     }
                               }
                          }
                      }
                  }
                catch (Exception e)
                {
                    System.out.println("Exception encountered.");
                    e.printStackTrace();            
                }
            }
        %>

        <%
        try
        {
            String data  = (String) request.getAttribute("ACSSAML");

            DocumentBuilder docBuilder;
            Document doc = null;
            DocumentBuilderFactory docBuilderFactory = DocumentBuilderFactory.newInstance();
            docBuilderFactory.setIgnoringElementContentWhitespace(true);
            docBuilder = docBuilderFactory.newDocumentBuilder();
            byte[] xmlDATA = data.getBytes();

            ByteArrayInputStream in = new ByteArrayInputStream(xmlDATA);
            doc = docBuilder.parse(in);
            doc.getDocumentElement().normalize();

            // Iterate hello child nodes of hello doc.
            NodeList list = doc.getChildNodes();

            for (int i=0; i < list.getLength(); i++)
            {
                displaySAMLInfo(list.item(i), "", out);
            }
        }
        catch (Exception e)
        {
            out.println("Exception encountered.");
            e.printStackTrace();
        }

        %>
    </body>
    </html>

## <a name="run-hello-application"></a><span data-ttu-id="eaf81-125">Uruchamianie aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="eaf81-125">Run hello application</span></span>
1. <span data-ttu-id="eaf81-126">Uruchom aplikację w emulatorze komputera hello lub wdrożyć tooAzure przy użyciu hello czynności opisane w [jak tooAuthenticate sieci Web użytkownikom Eclipse przy użyciu usługi kontroli dostępu platformy Azure](active-directory-java-authenticate-users-access-control-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="eaf81-126">Run your application in hello computer emulator or deploy tooAzure, using hello steps documented at [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span></span>
2. <span data-ttu-id="eaf81-127">Uruchom przeglądarkę i Otwórz aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="eaf81-127">Launch a browser and open your web application.</span></span> <span data-ttu-id="eaf81-128">Po zalogowaniu aplikacji tooyour zobaczysz informacje SAML, w tym potwierdzenia zabezpieczeń hello udostępniane przez dostawcę tożsamości hello.</span><span class="sxs-lookup"><span data-stu-id="eaf81-128">After you log on tooyour application, you'll see SAML information, including hello security assertion provided by hello identity provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eaf81-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eaf81-129">Next steps</span></span>
<span data-ttu-id="eaf81-130">toofurther poznać funkcje usług ACS i tooexperiment z bardziej zaawansowanych scenariuszy, zobacz [2.0 usługi kontroli dostępu][Access Control Service 2.0].</span><span class="sxs-lookup"><span data-stu-id="eaf81-130">toofurther explore ACS's functionality and tooexperiment with more sophisticated scenarios, see [Access Control Service 2.0][Access Control Service 2.0].</span></span>

[Prerequisites]: #pre
[Modify hello JSP file toodisplay SAML]: #modify_jsp
[Add hello JspWriter library tooyour build path and deployment assembly]: #add_library
[Run hello application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
