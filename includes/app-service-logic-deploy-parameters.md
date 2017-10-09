Usługi Azure Resource Manager Zdefiniuj parametry dla wartości ma toospecify po wdrożeniu hello szablonu. Szablon Hello zawiera sekcji parametrów zawierający wszystkie hello wartości parametrów.
Należy zdefiniować parametr dla tych wartości, które będą się różnić na podstawie hello projektu, który jest wdrażany lub opartych na środowisku hello, który jest wdrażany z. Definiuje parametry dla wartości, które będą zawsze hello takie same. Każda wartość parametru jest używany w hello szablonu toodefine powitalne zasoby, które są wdrażania. 

Określając parametry, użyj hello **allowedValues** toospecify pola, które wartości użytkownika można podać podczas wdrażania. Użyj hello **defaultValue** tooassign pola parametru toohello wartości, jeśli wartość nie zostanie podana podczas wdrażania.

Firma Microsoft będzie opisywać każdego parametru w szablonie hello.

### <a name="logicappname"></a>logicAppName
Nazwa Hello toocreate aplikacji logiki hello.

    "logicAppName": {
        "type": "string"
    }