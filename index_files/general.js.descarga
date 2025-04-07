// #region Documentation
// History
// v3.33[4]   marvin.rojas - PCRC - 13_Marzo_2018
//            Caso #91339  - Se crean funciones StorageToken,RegisterError
// v3.33[3]   david.cubero - PCRC - 22_Noviembre_2017
//            Caso #69484  - Se crean funciones SaveJsonLocalStorage, SaveKeyValueLocalStorage, GetLocalStorage
// v3.31[2]   luis.cespedes - PFCTI - 17_Julio_2017
//            Caso#68693 - Se modifica la función LockPage para ubicarla en el masterPage.
// v3.31[1]   ricardo.orozco - PFCTI - 05_Julio_2017
//            Caso#68693 - Creación de script

// #endregion Documentation

var globalError = {
    'Message': '',
    'statusText': '',
    'status': '',
    'functionName': '',
    'url': ''
};

function LockPage(lockPageDiv) {
    document.body.style.cursor = 'wait';
    $('#' + lockPageDiv).append('<div id="_lockPageDiv" style="background:white; position: fixed;top:0;left:0; margin-top: 100px; width: 100%;height:100%;z-index: 100001;opacity:0.1;filter: alpha(opacity = 1)"></div>');
}

function UnlockPage() {
    document.body.style.cursor = 'default';    
    $("#_lockPageDiv").remove();

}

function SaveJsonLocalStorage(data) {
    try {    
        if (data == null) {
            return;
        }

        var dataParse = JSON.parse(data);
        var vKey, vValue;

        for (var i = 0; i < dataParse.length; i++) {
            vKey = dataParse[i].Key;
            vValue = dataParse[i].Value;
            window.localStorage.setItem(vKey, vValue);
        }
    } catch (e) {
        console.log(e);
    }
}
function SaveKeyValueLocalStorage(Key, Value) {
    try {
        if (Key !== null || Key !== '' || Key !== undefined || Key !== "") {
            window.localStorage.setItem(Key, Value);
        }
            
    } catch (e) {
        console.log(e);
    }
}

function GetLocalStorage(key) {
    try {
        return window.localStorage.getItem(key);
    } catch (e) {
        console.log(e);
    }
}


function StorageToken(Token) {
    if (Token != "") {
        window.localStorage.setItem("token", Token);
    }
}

function RegisterError(requestError, params, funcName, url) {
    var vUrl = globalBaseUrl + "shared/webservice/GlobalService.asmx/RegisterLogClientSide";   
    var resText = { Message: "Error undefined" };
    var vToken = GetLocalStorage("token");
    try {
        if (requestError != null) {
            if (requestError.responseText != "" && requestError.responseText != undefined) {
                resText = jQuery.parseJSON(requestError.responseText);
            }
            globalError.Message = resText.Message;
            globalError.statusText = requestError.statusText;
            globalError.status = requestError.status;
            globalError.functionName = funcName;
            globalError.url = url;            
        }

        var vData = JSON.stringify({ ErrorDetail: globalError, Params: params });
        $.ajax({
            type: "POST",
            url: vUrl,
            data: vData,
            headers: {
                "auth-key": vToken
            },
            contentType: "application/json; charset=utf-8",
            dataType: "json",
            async: true,
            success: function (response) { console.log(response) },
            error: function (XMLHttpRequest, textStatus, errorThrown) {
                console.log(XMLHttpRequest);
                console.log(textStatus);
                console.log(errorThrown);
            }
        });
    }
    catch (e) {
        console.log(e);
    }
}

function RemoveSpecialChar(txtId) { 
    $(txtId).val($(txtId).val().replace(/[^a-z0-9\s]/gi, '').replace(/[_\s]/g, ' '));
}

function ShowHtmlSpinner(id) {
    $('#' + id).append('<div style="text-align: center; margin-top: 7px;"><div id="div_LoadingSpinner" style="display: inline;"><img alt="Por favor espere..." src="../../../shared/pictures/spinner.GIF" /><div style="text-align: center;"><span>Cargando por favor espere...</span></div></div></div>');   
}