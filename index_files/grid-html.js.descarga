var _ErrorMessage = '*En este momento no podemos realizar su solicitud, por favor intente nuevamente mas tarde.';

//========================================================================
//Funcion general para llamados ajax
function ajax(type, url, data, async, onSuccess, onError) {
    $.ajax({
        type: type,
        url: url,
        data: data,
        contentType: "application/json; charset=utf-8",
        dataType: "json",
        async: async,
        success: onSuccess,
        error: onError
    });
}


//========================================================================
/*Resultado del llamado .ajax cuando es success, utilizado para mostrar
los datos en el grid html.
-pResult: resultado retornado por el ajax,
-pCtGrid: control div al que se desea agregar los datos eje:'#ctGridPT',
-pCtPager: control div encargado de la paginación eje:'#divPager',
-pCtMessage: control para mostrar mensaje eje:'#clErrorMessage'
*/
function OnSuccess(pResult, pCtGrid, pCtPager, pCtMessage) {
    try {
        $(pCtGrid).empty();

        if (pResult.d == null) {
            return;
        }

        if (pResult.d[0].length === 1) {
            ShowMessage(pCtMessage, pResult.d);
            return;
        }

        var vKey, vValue, vPagination, vTable, vFooter, vPageIndex, vPageSize, vRecordCount, vLoadPagination;

        for (var i = 0; i < pResult.d.length; i++) {
            vKey = pResult.d[i].Key;
            vValue = pResult.d[i].Value;

            switch (vKey) {
                case "ErrorMessage":
                    ShowMessage(pCtMessage, vValue);
                    return;
                case "Pagination":
                    vPagination = vValue;
                    break;
                case "Table":
                case "Body":
                    vTable = vValue;
                    break;
                case "Footer":
                    vFooter = vValue;
                    break;
                case "PageIndex":
                    vPageIndex = vValue;
                    break;
                case "PageSize":
                    vPageSize = vValue;
                    break;
                case "RecordCount":
                    vRecordCount = vValue;
                    break;
                case "LoadPagination":
                    vLoadPagination = vValue;
                    break;
            }
        }

        $(pCtGrid).append(vPagination);
        $(pCtGrid).append(vTable).hide().fadeIn(200);
        $(pCtGrid).append(vFooter);

        if (vLoadPagination != "False") {
            Pagination(pCtPager, parseInt(vPageIndex), parseInt(vPageSize), parseInt(vRecordCount));
        }

    } catch (e) {
        console.log(e);
    }
}

//========================================================================
/* Funcion para cargar multiples grids, resultado del llamado .ajax cuando
 es success, utilizado para mostrar los datos en el grid html.
-pResult: resultado retornado por el ajax,
-pCtGrid: control div al que se desea agregar los datos eje:'#ctGridPT',
-pCtPager: control div encargado de la paginación eje:'#divPager',
-pCtMessage: control para mostrar mensaje eje:'#clErrorMessage'
*/
function OnSuccessLst(pResult, pCtPager, pCtMessage) {
    try {

        pResult = pResult.d || pResult;

        if (pResult == null) {
            return;
        }

        var vKey, vValue, vPagination, vTable, vFooter, vPageIndex, vPageSize, vRecordCount, vGridId, vLoadPagination, vCtPager;

        for (var i = 0; i < pResult.length; i++) {

            if ($.isArray(pResult[i])) {

                for (var j = 0; j < pResult[i].length; j++) {

                    vKey = pResult[i][j].Key;
                    vValue = pResult[i][j].Value;

                    switch (vKey) {
                        case "ErrorMessage":
                            ShowMessage(pCtMessage, vValue);
                            return;
                        case "Pagination":
                            vPagination = vValue;
                            break;
                        case "Table":
                        case "Body":
                            vTable = vValue;
                            break;
                        case "Footer":
                            vFooter = vValue;
                            break;
                        case "PageIndex":
                            vPageIndex = vValue;
                            break;
                        case "PageSize":
                            vPageSize = vValue;
                            break;
                        case "RecordCount":
                            vRecordCount = vValue;
                            break;
                        case "GridId":
                            vGridId = vValue;
                            break;
                        case "LoadPagination":
                            vLoadPagination = vValue;
                            break;
                        case "Pager":
                            vCtPager = vValue;
                            break;
                    }
                }

                $(vGridId).empty();
                $(vGridId).append(vPagination);
                $(vGridId).append(vTable).hide().fadeIn('fast');
                $(vGridId).append(vFooter);

                if (vLoadPagination != "False") {
                    vCtPager = pCtPager || vCtPager;
                    Pagination(vCtPager, parseInt(vPageIndex), parseInt(vPageSize), parseInt(vRecordCount));
                }
            }
            else {
                if (pResult.length === 0 || pResult.length === undefined || typeof pResult[i] === "string") {
                    ShowMessage(pCtMessage, pResult[i]);
                }
            }
        }

    } catch (e) {
        console.log(e);
    }
}
//========================================================================
/*Resultado del llamado .ajax cuando es error
-pCtMessage: control para mostrar mensaje eje:'#clErrorMessage'
*/
function AjaxError(pRequest, pCtMessage) {
    try {
        if (pRequest.status === 401) {
            window.location = globalBaseUrl + "/PB/pages/administration/NoSessionPage.aspx";
        } else {
            if (pRequest != null && pRequest.responseText != "") {
                var r = jQuery.parseJSON(pRequest.responseText);
                ShowMessage(pCtMessage, _ErrorMessage);
                console.log(r.Message);
            }
        }
    } catch (e) {
        console.log(e);
    }
}

//========================================================================
/*Función que se utiliza para la paginación del grid html 
-pCtPager: control div encargado de la paginación
-pPageIndex: número de página
-pPageSize: Cantidad de registros por página
-pRecordCount: Total de registros
*/
function Pagination(pCtPager, pPageIndex, pPageSize, pRecordCount) {
    try {
        $(pCtPager).ASPSnippets_Pager({
            ActiveCssClass: "current",
            PagerCssClass: "pager",
            PageIndex: parseInt(pPageIndex),
            PageSize: parseInt(pPageSize),
            RecordCount: parseInt(pRecordCount)
        });
    } catch (e) {
        console.log(e);
    }
}
//========================================================================
/*Función que se utiliza para guardar en un hiddenfield la selección 
concatenado por "," en caso que el grid tenga una columna checkbox.
-pElem: control checkbox, se envia "this",
-pCtNameHF: nombre del control hiddenfield eje: 'hfConsecutive'
*/
var arrChecked = [];
function Checked(pElem, pCtNameHF) {
    try {
        var selected = pCtNameHF,
            consecutive = pElem ? (pElem.id).toString() : "";

        if (pElem.checked) {
            if (selected.value === "") {
                arrChecked = new Array();
            } else {
                arrChecked = selected.value.split(",");
            }
            if ($.inArray(consecutive, arrChecked) < 0) {
                arrChecked.push(consecutive);
            }
            selected.value = arrChecked.join(",");
        } else {
            arrChecked = selected.value.split(",");
            for (var i = 0; i < arrChecked.length; i++) {
                if (arrChecked[i] === pElem.id) {
                    arrChecked.splice(i, 1);
                    selected.value = arrChecked.join(",");
                }
            }
        }
    } catch (e) {
        console.log(e);
    }
}
//========================================================================
/*Función que se utiliza para mostrar mensajes.
-pCt: nombre del control eje:'#clErrorMessage',
-pMessage: mensaje que se desea mostrar
*/
function ShowMessage(pCt, pMessage) {
    try {
        if (pMessage && typeof pMessage === 'string' && pMessage.length > 0) {
            $(pCt).text(pMessage);
            $(pCt).show();
        }
    } catch (e) {
        console.log(e);
    }
}
//========================================================================
/*Función que se utiliza para ocultar mensajes.
-pCt: nombre del control
*/
function HideMessageById(pCt) {
    try {
        $(pCt).text("");
        $(pCt).hide();
    } catch (e) {
        console.log(e);
    }
}
//========================================================================
/*Oculta el div de progress*/
function HideLoading() {
    try {
        var vBackDiv = document.getElementById("BackDiv");
        var vLoadingDiv = document.getElementById("LoadingDiv");
        if (vBackDiv != null && vLoadingDiv != null) {
            vBackDiv.style.display = "none";
            vLoadingDiv.style.display = "none";
        }
    } catch (e) {
        console.log(e);
    }
}