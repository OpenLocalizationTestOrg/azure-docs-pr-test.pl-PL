---
title: "Samouczek aplikacji sieci web platformy Flask aaaPython dla bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Przejrzyj samouczek bazy danych przy użyciu bazy danych Azure rozwiązania Cosmos toostore i dostępu do danych z aplikacji sieci web platformy Python Flask hostowanej na platformie Azure. Znajdź rozwiązania do tworzenia aplikacji."
keywords: Application development, python flask, python web application, python web development
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 20ebec18-67c2-4988-a760-be7c30cfb745
ms.service: cosmos-db
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/09/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 87b73c656ed96a7efbd162843a1529d435f027f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-python-flask-web-application-using-azure-cosmos-db"></a>Tworzenie aplikacji internetowej platformy Python Flask za pomocą usługi Azure Cosmos DB
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

Ten samouczek pokazuje, jak toouse danych toostore i dostępu do bazy danych Azure rozwiązania Cosmos w języku Python hostowanej na platformie Azure aplikacji sieci web i przyjęto założenie, że ma pewne doświadczenie w korzystaniu z języka Python i witryn sieci Web Azure.

Ten samouczek bazy danych obejmuje następujące zagadnienia:

1. Tworzenie i Inicjowanie obsługi konta DB rozwiązania Cosmos.
2. Tworzenie aplikacji platformy Python Flask.
3. Łączenie tooand przy użyciu rozwiązania Cosmos bazy danych z aplikacji sieci web.
4. Wdrażanie tooAzure aplikacji sieci web hello.

W ramach tego samouczka, utworzysz prostą aplikację do głosowania umożliwiający toovote w ankiecie.

![Zrzut ekranu przedstawiający aplikację do głosowania hello utworzone przez tego samouczka bazy danych](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)

## <a name="database-tutorial-prerequisites"></a>Wymagania wstępne dotyczące samouczka
Przed rozpoczęciem powitalne instrukcje w tym artykule, należy upewnij się, że mają zainstalowane następujące hello:

* Aktywne konto platformy Azure. Jeśli jej nie masz, możesz utworzyć bezpłatne konto próbne w zaledwie kilka minut. Aby uzyskać szczegółowe informacje, zobacz [Bezpłatna wersja próbna platformy Azure](https://azure.microsoft.com/pricing/free-trial/).
 
    LUB 

    Lokalna instalacja hello [Azure rozwiązania Cosmos DB emulatora](local-emulator.md).
* [Microsoft Visual Studio Community 2017](http://www.visualstudio.com/).  
* [Python Tools for Visual Studio](https://github.com/Microsoft/PTVS/).  
* [Zestaw Microsoft Azure SDK for Python 2.7](https://azure.microsoft.com/downloads/). 
* [Python 2.7.13](https://www.python.org/downloads/windows/). 

> [!IMPORTANT]
> Jeśli instalujesz środowisko Python 2.7 dla powitania po raz pierwszy, upewnij się, na ekranie powitania dostosować Python 2.7.13 wybranym **dodać python.exe tooPath**.
> 
> ![Zrzut ekranu przedstawiający ekran Dostosowywanie środowiska Python 2.7.11 hello, których należy tooselect Add python.exe tooPath](./media/documentdb-python-application/cosmos-db-python-install.png)
> 
> 

* [Microsoft Visual C++ Compiler for Python 2.7](https://www.microsoft.com/en-us/download/details.aspx?id=44266).

## <a name="step-1-create-an-azure-cosmos-db-database-account"></a>Krok 1. Tworzenie konta bazy danych usługi Azure Cosmos DB
Zacznijmy od utworzenia konta usługi Cosmos DB. Jeśli już masz konto lub jeśli używasz hello Azure rozwiązania Cosmos DB emulatora w tym samouczku, można pominąć zbyt[krok 2: Tworzenie nowej aplikacji sieci web platformy Python Flask](#step-2-create-a-new-python-flask-web-application).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<br/>
Teraz przejdziemy przez jak toocreate nowej aplikacji sieci web platformy Python Flask od hello tła w.

## <a name="step-2-create-a-new-python-flask-web-application"></a>Krok 2. Tworzenie nowej aplikacji sieci Web platformy Python Flask
1. W programie Visual Studio na powitania **pliku** menu punktu zbyt**nowy**, a następnie kliknij przycisk **projektu**.
   
    Witaj **nowy projekt** zostanie wyświetlone okno dialogowe.
2. W okienku po lewej stronie powitania, rozwiń węzeł **szablony** , a następnie **Python**, a następnie kliknij przycisk **Web**. 
3. Wybierz **projektu sieci Web platformy Flask** hello środkowym okienku, a następnie w hello **nazwa** wpisz **samouczek**, a następnie kliknij przycisk **OK**. Pamiętaj, że nazwy pakietów języka Python powinny być tylko małe litery, zgodnie z opisem w hello [Przewodnik po stylu kodu Python](https://www.python.org/dev/peps/pep-0008/#package-and-module-names).
   
    Te nowe tooPython Flask jest platforma programistyczna aplikacji sieci web, ułatwiające szybsze tworzenie aplikacji sieci web w języku Python.
   
    ![Zrzut ekranu okna nowy projekt hello w programie Visual Studio wyróżnione na powitania po lewej, projekt sieci Web platformy Flask Python wybrany w środku hello i hello nazwą tutorial w polu Nazwa hello języka Python](./media/documentdb-python-application/image9.png)
4. W hello **narzędzi Python Tools for Visual Studio** okna, kliknij przycisk **zainstalować w środowisku wirtualnym**. 
   
    ![Zrzut ekranu samouczka bazy danych hello — narzędzia Python Tools for Visual Studio okna](./media/documentdb-python-application/python-install-virtual-environment.png)
5. W hello **Dodawanie środowiska wirtualnego** okna, można zaakceptować ustawienia domyślne hello i użyć środowiska Python 2.7 jako podstawowego środowiska hello, ponieważ pakiet PyDocumentDB nie obsługuje obecnie środowiska Python 3.x, a następnie kliknij przycisk **Utwórz**. Konfiguruje środowisko wirtualne języka Python hello wymagane dla projektu.
   
    ![Zrzut ekranu samouczka bazy danych hello — narzędzia Python Tools for Visual Studio okna](./media/documentdb-python-application/image10_A.png)
   
    Wyświetla okno danych wyjściowych Hello `Successfully installed Flask-0.10.1 Jinja2-2.8 MarkupSafe-0.23 Werkzeug-0.11.5 itsdangerous-0.24 'requirements.txt' was installed successfully.` po pomyślnym zainstalowaniu środowiska hello.

## <a name="step-3-modify-hello-python-flask-web-application"></a>Krok 3: Modyfikowanie aplikacji sieci web platformy Python Flask hello
### <a name="add-hello-python-flask-packages-tooyour-project"></a>Dodaj projekt tooyour pakietów platformy Python Flask hello
Po skonfigurowaniu projektu musisz tooadd hello wymagane Flask pakiety tooyour projektu, w tym pydocumentdb — pakiet języka Python hello usługi documentdb.

1. W Eksploratorze rozwiązań Otwórz plik hello o nazwie **requirements.txt** i Zastąp zawartość hello hello następujące czynności:
   
        flask==0.9
        flask-mail==0.7.6
        sqlalchemy==0.7.9
        flask-sqlalchemy==0.16
        sqlalchemy-migrate==0.7.2
        flask-whooshalchemy==0.55a
        flask-wtf==0.8.4
        pytz==2013b
        flask-babel==0.8
        flup
        pydocumentdb>=1.0.0
2. Zapisz hello **requirements.txt** pliku. 
3. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy pozycję **env**, a następnie kliknij polecenie **Zainstaluj z pliku requirements.txt**.
   
    ![Zrzut ekranu przedstawiający env (Python 2.7) wybrany w ramach instalacji z pliku requirements.txt wyróżnione na liście hello](./media/documentdb-python-application/cosmos-db-python-install-from-requirements.png)
   
    Po pomyślnej instalacji okno danych wyjściowych hello wyświetla następujące hello:
   
        Successfully installed Babel-2.3.2 Tempita-0.5.2 WTForms-2.1 Whoosh-2.7.4 blinker-1.4 decorator-4.0.9 flask-0.9 flask-babel-0.8 flask-mail-0.7.6 flask-sqlalchemy-0.16 flask-whooshalchemy-0.55a0 flask-wtf-0.8.4 flup-1.0.2 pydocumentdb-1.6.1 pytz-2013b0 speaklater-1.3 sqlalchemy-0.7.9 sqlalchemy-migrate-0.7.2
   
   > [!NOTE]
   > W rzadkich przypadkach można napotkać błąd w oknie danych wyjściowych hello. W takim przypadku należy sprawdzić, czy błąd hello jest toocleanup powiązane. Czasami Oczyszczanie hello nie powiedzie się, ale hello instalacja zakończy się pomyślnie (Przewiń w górę tooverify okno danych wyjściowych hello to). Można sprawdzić instalację przez [środowiska wirtualnego hello weryfikacji](#verify-the-virtual-environment). Jeśli hello instalacja nie powiodła się, ale hello weryfikacja zakończy się pomyślnie, jest OK toocontinue.
   > 
   > 

### <a name="verify-hello-virtual-environment"></a>Sprawdź hello środowiska wirtualnego
Upewnijmy się, że wszystko jest poprawnie zainstalowane.

1. Utworzenie rozwiązania hello naciskając **Ctrl**+**Shift**+**B**.
2. Po pomyślnym hello kompilacji, należy uruchomić hello witryny sieci Web, naciskając **F5**. To spowoduje uruchomienie serwera programistycznego platformy Flask hello i uruchomi przeglądarkę sieci web. Powinny pojawić się po stronie powitania.
   
    ![Witaj pusty platformy Python Flask projekt aplikacji sieci web wyświetlany w przeglądarce](./media/documentdb-python-application/image12.png)
3. Zatrzymaj debugowanie hello witryny sieci Web, naciskając klawisz **Shift**+**F5** w programie Visual Studio.

### <a name="create-database-collection-and-document-definitions"></a>Tworzenie definicji bazy danych, kolekcji i dokumentu
Teraz utwórzmy aplikację do głosowania przez dodanie nowych plików i zaktualizowanie pozostałych.

1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **samouczek** projektu, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **nowy element**. Wybierz **pusty plik Python** i nazwa pliku hello **forms.py**.  
2. Dodaj hello następującego pliku forms.py toohello kodu, a następnie zapisz plik hello.

```python
from flask.ext.wtf import Form
from wtforms import RadioField

class VoteForm(Form):
    deploy_preference  = RadioField('Deployment Preference', choices=[
        ('Web Site', 'Web Site'),
        ('Cloud Service', 'Cloud Service'),
        ('Virtual Machine', 'Virtual Machine')], default='Web Site')
```


### <a name="add-hello-required-imports-tooviewspy"></a>Dodaj hello wymaganych importów tooviews.py
1. W Eksploratorze rozwiązań rozwiń hello **samouczek** folderu, a następnie otwórz hello **views.py** pliku. 
2. Dodaj następujące instrukcje importu toohello góry hello hello **views.py** pliku, a następnie zapisz plik hello. Te zaimportowane spowoduje DB rozwiązania Cosmos i hello pakietów platformy Flask.
   
    ```python
    from forms import VoteForm
    import config
    import pydocumentdb.document_client as document_client
    ```

### <a name="create-database-collection-and-document"></a>Tworzenie bazy danych, kolekcji i dokumentu
* Nadal **views.py**, Dodaj hello kod zakończenia toohello hello pliku. Odpowiada on za tworzenie hello bazy danych używane przez hello formularza. Nie usuwaj żadnego kodu istniejących hello w **views.py**. Po prostu Dołącz toohello temu elementowi end.

```python
@app.route('/create')
def create():
    """Renders hello contact page."""
    client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

    # Attempt toodelete hello database.  This allows this toobe used toorecreate as well as create
    try:
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))
        client.DeleteDatabase(db['_self'])
    except:
        pass

    # Create database
    db = client.CreateDatabase({ 'id': config.DOCUMENTDB_DATABASE })

    # Create collection
    collection = client.CreateCollection(db['_self'],{ 'id': config.DOCUMENTDB_COLLECTION })

    # Create document
    document = client.CreateDocument(collection['_self'],
        { 'id': config.DOCUMENTDB_DOCUMENT,
          'Web Site': 0,
          'Cloud Service': 0,
          'Virtual Machine': 0,
          'name': config.DOCUMENTDB_DOCUMENT 
        })

    return render_template(
       'create.html',
        title='Create Page',
        year=datetime.now().year,
        message='You just created a new database, collection, and document.  Your old votes have been deleted')
```


### <a name="read-database-collection-document-and-submit-form"></a>Odczytywanie bazy danych, kolekcji i dokumentów oraz przesyłanie formularza
* Nadal **views.py**, Dodaj hello kod zakończenia toohello hello pliku. Odpowiada on za konfigurowanie formularza hello, odczytywanie hello bazy danych, kolekcji i dokumentu. Nie usuwaj żadnego kodu istniejących hello w **views.py**. Po prostu Dołącz toohello temu elementowi end.

```python
@app.route('/vote', methods=['GET', 'POST'])
def vote(): 
    form = VoteForm()
    replaced_document ={}
    if form.validate_on_submit(): # is user submitted vote  
        client = document_client.DocumentClient(config.DOCUMENTDB_HOST, {'masterKey': config.DOCUMENTDB_KEY})

        # Read databases and take first since id should not be duplicated.
        db = next((data for data in client.ReadDatabases() if data['id'] == config.DOCUMENTDB_DATABASE))

        # Read collections and take first since id should not be duplicated.
        coll = next((coll for coll in client.ReadCollections(db['_self']) if coll['id'] == config.DOCUMENTDB_COLLECTION))

        # Read documents and take first since id should not be duplicated.
        doc = next((doc for doc in client.ReadDocuments(coll['_self']) if doc['id'] == config.DOCUMENTDB_DOCUMENT))

        # Take hello data from hello deploy_preference and increment our database
        doc[form.deploy_preference.data] = doc[form.deploy_preference.data] + 1
        replaced_document = client.ReplaceDocument(doc['_self'], doc)

        # Create a model toopass tooresults.html
        class VoteObject:
            choices = dict()
            total_votes = 0

        vote_object = VoteObject()
        vote_object.choices = {
            "Web Site" : doc['Web Site'],
            "Cloud Service" : doc['Cloud Service'],
            "Virtual Machine" : doc['Virtual Machine']
        }
        vote_object.total_votes = sum(vote_object.choices.values())

        return render_template(
            'results.html', 
            year=datetime.now().year, 
            vote_object = vote_object)

    else :
        return render_template(
            'vote.html', 
            title = 'Vote',
            year=datetime.now().year,
            form = form)
```


### <a name="create-hello-html-files"></a>Utwórz hello pliki HTML
1. W Eksploratorze rozwiązań w hello **samouczek** powitania kliknij folder prawym **szablony** folderu, kliknij przycisk **Dodaj**, a następnie kliknij przycisk **nowy element**. 
2. Wybierz **strony HTML**, a następnie wpisz nazwę hello **create.html**. 
3. Powtórz kroki 1 i 2 toocreate dwa dodatkowe pliki HTML: results.html i vote.html.
4. Dodaj hello zbyt następującego kodu**create.html** w hello `<body>` elementu. Służy do wyświetlania komunikatu informującego o tym, że utworzyliśmy nową bazę danych, kolekcję i dokument.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>{{ title }}.</h2>
    <h3>{{ message }}</h3>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```
5. Dodaj hello zbyt następującego kodu**results.html** w hello `<body`> elementu. Wyświetla wyniki hello hello sondowania.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Results of hello vote</h2>
        <br />
   
    {% for choice in vote_object.choices %}
    <div class="row">
        <div class="col-sm-5">{{choice}}</div>
            <div class="col-sm-5">
                <div class="progress">
                    <div class="progress-bar" role="progressbar" aria-valuenow="{{vote_object.choices[choice]}}" aria-valuemin="0" aria-valuemax="{{vote_object.total_votes}}" style="width: {{(vote_object.choices[choice]/vote_object.total_votes)*100}}%;">
                                {{vote_object.choices[choice]}}
                </div>
            </div>
            </div>
    </div>
    {% endfor %}
   
    <br />
    <a class="btn btn-primary" href="{{ url_for('vote') }}">Vote again?</a>
    {% endblock %}
    ```
6. Dodaj hello zbyt następującego kodu**vote.html** w hello `<body`> elementu. On wyświetla hello sondowania i akceptuje hello głosów. Po zarejestrowaniu głosów hello, hello kontrola jest przekazywana tooviews.py gdzie możemy rozpozna hello głos jest rozpoznawany i odpowiednio Dołącz hello dokumentu.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>What is your favorite way toohost an application on Azure?</h2>
    <form action="" method="post" name="vote">
        {{form.hidden_tag()}}
            {{form.deploy_preference}}
            <button class="btn btn-primary" type="submit">Vote</button>
    </form>
    {% endblock %}
    ```
7. W hello **szablony** folderu, Zastąp zawartość hello **index.html** następujący hello. Służy to jako hello początkowej strony aplikacji.
   
    ```html
    {% extends "layout.html" %}
    {% block content %}
    <h2>Python + Azure Cosmos DB Voting Application.</h2>
    <h3>This is a sample Cosmos DB voting application using PyDocumentDB</h3>
    <p><a href="{{ url_for('create') }}" class="btn btn-primary btn-large">Create/Clear hello Voting Database &raquo;</a></p>
    <p><a href="{{ url_for('vote') }}" class="btn btn-primary btn-large">Vote &raquo;</a></p>
    {% endblock %}
    ```

### <a name="add-a-configuration-file-and-change-hello-initpy"></a>Dodaj plik konfiguracji i zmień hello \_ \_init\_\_.py
1. W Eksploratorze rozwiązań kliknij prawym przyciskiem myszy hello **samouczek** projektu, kliknij przycisk **Dodaj**, kliknij przycisk **nowy element**, wybierz pozycję **pusty plik Python**, a następnie Nazwa pliku hello **config.py**. Ten plik konfiguracji jest wymagany przez formularze na platformie Flask. Służy on tooprovide także klucz tajny. Ten klucz nie jest jednak potrzebny w tym samouczku.
2. Dodaj następujące hello tooconfig.py kodu, musisz tooalter hello wartości **DOCUMENTDB\_hosta** i **DOCUMENTDB\_klucza** w następnym kroku hello.
   
    ```python
    CSRF_ENABLED = True
    SECRET_KEY = 'you-will-never-guess'
   
    DOCUMENTDB_HOST = 'https://YOUR_DOCUMENTDB_NAME.documents.azure.com:443/'
    DOCUMENTDB_KEY = 'YOUR_SECRET_KEY_ENDING_IN_=='
   
    DOCUMENTDB_DATABASE = 'voting database'
    DOCUMENTDB_COLLECTION = 'voting collection'
    DOCUMENTDB_DOCUMENT = 'voting document'
    ```
3. W hello [portalu Azure](https://portal.azure.com/), przejdź toohello **klucze** bloku, klikając **Przeglądaj**, **kont DB rozwiązania Cosmos Azure**, kliknij dwukrotnie nazwę hello z hello toouse konta, a następnie kliknij przycisk hello **klucze** przycisku na powitania **Essentials** obszaru. W hello **klucze** bloku, hello kopiowania **URI** wartość i wklej go do hello **config.py** pliku jako wartość hello hello **DOCUMENTDB\_hosta**  właściwości. 
4. W portalu Azure w hello hello **klucze** bloku kopia wartość hello hello **klucza podstawowego** lub hello **klucza pomocniczego**i wklej go do hello **config.py**  pliku jako wartość hello hello **DOCUMENTDB\_klucza** właściwości.
5. W hello  **\_ \_init\_\_.py** plików, dodawanie hello następującego wiersza. 
   
        app.config.from_object('config')
   
    Tak, aby zawartość pliku hello hello jest:
   
    ```python
    from flask import Flask
    app = Flask(__name__)
    app.config.from_object('config')
    import tutorial.views
    ```
6. Po dodaniu wszystkich plików hello, Eksplorator rozwiązań powinien wyglądać następująco:
   
    ![Zrzut ekranu przedstawiający okno programu Visual Studio Solution Explorer hello](./media/documentdb-python-application/cosmos-db-python-solution-explorer.png)

## <a name="step-4-run-your-web-application-locally"></a>Krok 4. Uruchamianie aplikacji sieci Web lokalnie
1. Utworzenie rozwiązania hello naciskając **Ctrl**+**Shift**+**B**.
2. Po pomyślnym hello kompilacji, należy uruchomić hello witryny sieci Web, naciskając **F5**. Następujące hello powinny zostać wyświetlone na ekranie.
   
    ![Zrzut ekranu przedstawiający Witaj Python + Azure rozwiązania Cosmos głosowania aplikacji DB wyświetlany w przeglądarce sieci web](./media/documentdb-python-application/cosmos-db-pythonr-run-application.png)
3. Kliknij przycisk **Utwórz/wyczyść hello głosowania bazy danych** toogenerate hello w bazie danych.
   
    ![Zrzut ekranu przedstawiający hello strony tworzenia aplikacji sieci web hello — szczegóły programowania](./media/documentdb-python-application/cosmos-db-python-run-create-page.png)
4. Następnie kliknij przycisk **Vote** (Głosuj) i wybierz jedną z opcji.
   
    ![Zrzut ekranu przedstawiający hello aplikacji sieci web z pytaniem, które należy udzielić odpowiedzi](./media/documentdb-python-application/cosmos-db-vote.png)
5. Dla każdego oddany głos powoduje zwiększenie odpowiedniego licznika hello.
   
    ![Zrzut ekranu przedstawiający hello wyniki wyświetlane stronie głosowania hello](./media/documentdb-python-application/cosmos-db-voting-results.png)
6. Zatrzymaj debugowanie projektu hello, naciskając klawisz Shift + F5.

## <a name="step-5-deploy-hello-web-application-tooazure"></a>Krok 5: Wdrożenie tooAzure aplikacji sieci web hello
Teraz, gdy masz hello kompletna aplikacja działa poprawnie z rozwiązania Cosmos DB zamierzamy toodeploy to tooAzure.

1. Kliknij prawym przyciskiem myszy projekt hello w Eksploratorze rozwiązań (Upewnij się, że nie masz uruchomiony lokalnie) i wybierz **publikowania**.  
   
     ![Zrzut ekranu samouczka hello zaznaczone w Eksploratorze rozwiązań z wyróżnioną opcją publikowania hello](./media/documentdb-python-application/image20.png)
2. W hello **publikowania** okno dialogowe, wybierz opcję **Microsoft Azure App Service**, wybierz pozycję **Utwórz nowy**, a następnie kliknij przycisk **publikowania**.
   
    ![Zrzut ekranu okna publikowanie w sieci Web hello z wyróżnionym programem Microsoft Azure App Service](./media/documentdb-python-application/cosmos-db-python-publish.png)
3. W hello **Tworzenie usługi App Service** okna dialogowego wprowadź nazwę powitania dla aplikacji sieci web, wraz z Twojej **subskrypcji**, **grupy zasobów**, i **planu usługi App Service** , następnie kliknij przycisk **Utwórz**.
   
    ![Zrzut ekranu okna hello okno aplikacji sieci Web programu Microsoft Azure](./media/documentdb-python-application/cosmos-db-python-create-app-service.png)
4. W ciągu kilku sekund program Visual Studio zakończy publikowanie aplikacji usługi i uruchomi przeglądarkę, w którym można zobaczyć Twojej handiwork działające na platformie Azure!

    ![Zrzut ekranu okna hello okno aplikacji sieci Web programu Microsoft Azure](./media/documentdb-python-application/cosmos-db-python-appservice-created.png)

## <a name="troubleshooting"></a>Rozwiązywanie problemów
Jeśli jest to hello na komputerze uruchomiono pierwszej aplikacji Python, upewnij się, następujących hello foldery (lub hello odpowiadające im lokalizacje instalacji) są uwzględnione w zmiennej PATH:

    C:\Python27\site-packages;C:\Python27\;C:\Python27\Scripts;

Jeśli wystąpi błąd na stronie głosowania, a nazwa projektu jest coś innego niż **samouczek**, upewnij się, że  **\_ \_init\_\_.py** Popraw nazwę projektu w wierszu hello hello odwołania: `import tutorial.view`.

## <a name="next-steps"></a>Następne kroki
Gratulacje! Ma wystarczy wykonać swoją pierwszą aplikację sieci web języka Python za pomocą rozwiązania Cosmos bazy danych i opublikować ją tooAzure.

Często aktualizujemy i poprawiamy ten temat na podstawie opinii czytelników.  Po ukończeniu samouczka hello, należy za pomocą hello głosowania przyciski na powitania góry i u dołu tej strony oraz być tooinclude się swoją opinię na jakie ulepszenia ma toosee wprowadzone. Jeśli chcesz nam toocontact bezpośrednio, uważasz, że tooinclude wolnego adresu e-mail w komentarzach.

Aplikacja sieci web tooyour tooadd dodatkowe funkcje, przejrzyj hello interfejsami API dostępnymi w hello [Azure rozwiązania Cosmos DB Python SDK](documentdb-sdk-python.md).

Aby uzyskać więcej informacji na temat platformy Azure, programu Visual Studio i języka Python, zobacz hello [Centrum deweloperów języka Python](https://azure.microsoft.com/develop/python/). 

Aby uzyskać dodatkowe samouczki platformy Python Flask, zobacz [hello Flask Mega-Tutorial, Part I: Hello, World!](http://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world). 

[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[2]: https://www.python.org/downloads/windows/
[3]: https://www.microsoft.com/download/details.aspx?id=44266
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Azure portal]: http://portal.azure.com
