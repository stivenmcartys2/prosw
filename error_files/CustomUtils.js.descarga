// #region Documentation
// MUY IMPORTANTE:
//     ESTE SCRIPT NO DEBE SER GENERADO EN RELEASE, 
//     A CADA BANCO SE LE DEBE HACER UNA IMPLEMENTACIÓN PERSONALIZADA
// History
// v3.29[3]   marvin.rojas - PFCTI - 26_Septiembre_2016
//            Caso#65908   - Se  modifica script validatecontrolMail
// v3.28[2]   marvin.rojas - PFCTI - 23_Agosto_2016
//            Caso#66185   - Se  modifica script validatecontrol
// v3.27 [1]  marvin.rojas - PFCTI - 14_Marzo_2014
//           Caso#64985 - Se crea script  para pasar a mayuscula los campos de texto .
// v3.4.5 [0]  diego.solano - SGAL - 23_Octubre_2014
//           Caso#56901 - Se elimina método ShowWrongBrowserMsg el cual no se utiliza.
// v3.0.19.1 victor.viquez - SGAL - 04_Mayo_2011
//           Ajustes para incorporación de caracteres especiales en función zGetNumPadLayout.

// #endregion Documentation

// #region VirtualKeyboard

// Retorna los arreglos de caracteres a utilizar
// SpecialArray con los caracteres especiales a mostrar
// NumArray con los números a mostrar
// CharArray con las letras a mostrar
function zGetCharArrays () {
    var vSpecialArray = new Array(["#","#"],["$","$"],["%","%"]);
    var vNumArray = new Array(["0","0"], ["1","1"], ["2","2"], ["3","3"], ["4","4"], ["5","5"], ["6","6"], ["7","7"], ["8","8"], ["9","9"]);
    var vCharArray = new Array(["q", "Q"], ["w", "W"], ["e", "E"], ["r", "R"], ["t", "T"], ["y", "Y"], ["u", "U"], ["i", "I"], ["o", "O"], ["p", "P"],
                              ["a", "A"], ["s", "S"], ["d", "D"], ["f", "F"], ["g", "G"], ["h", "H"], ["j", "J"], ["k", "K"], ["l", "L"],
                              ["z", "Z"], ["x", "X"], ["c", "C"], ["v", "V"], ["b", "B"], ["n", "N"], ["m", "M"] );

    return {SpecialArray: vSpecialArray, NumArray : vNumArray, CharArray : vCharArray}
}

// Retorna parámetros de configuración del teclado
//  Shuffle: true ordenar el teclado random, false = layout normal
//  TabDisabled = true = tab inactivo, false = tab activo
//  TabDisabledMsg = mensaje que será mostrado con el tab inactivo
//  UpperCase = true presenta letras en mayúscula, false mayúsculas y minúsculas
//  DisplayKey = false no muestra confirmación de tecla presionada, de otra forma true
//  DisplayKeyWait = tiempo de espera para limpiar la tecla mostrada
//  DisplayKeyZoneAutoHide = true el área donde la tecla está mostrada desaparecerá tan pronto como se dé el timeout
function zGetSettings () {
  return {
     Shuffle : true,
     TabDisabled : true,
     TabDisabledMsg : "Tecla deshabilitada",
     UpperCase : true,
     DisplayKey : false,
     DisplayKeyWait : 500,
     DisplayKeyZoneAutoHide : false,
     ValidateMaxLength : false,
     MaxLengthAlertMessage : "Ha llegado al limite de caracteres permitido"
  }
}

// Retorna los caracteres que se visualizarán en el teclado
// pNumSpecialArray: arreglo de caracteres numéricos
// pCharArray: arreglo de caracteres
function zGetSpaVKI_Layout (pNumSpecialArray, pCharArray) {
    return [
      [["\u00ba", "\u00aa", "\\"], pNumSpecialArray.shift(), pNumSpecialArray.shift(), pNumSpecialArray.shift(), pNumSpecialArray.shift(), pNumSpecialArray.shift(), pNumSpecialArray.shift(), pNumSpecialArray.shift(), pNumSpecialArray.shift(), pNumSpecialArray.shift(), pNumSpecialArray.shift(), ["'", "?"], ["\u00a1", "\u00bf"], ["Bksp", "Bksp"]],
      [["Tab", "Tab"], pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), ["\u0060", "^", "["], ["\u002b", "\u002a", "]"], ["Enter", "Enter"]],
      [["Caps", "Caps"], pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), ["\u00f1", "\u00d1"], ["\u00b4", "\u00a8", "{"], ["\u00e7", "\u00c7", "}"]],
      [["Shift", "Shift"], ["<", ">"], pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), [",", ";"], [".", ":"], ["-", "_"], ["Shift", "Shift"]],
      [[" ", " ", " ", " "], ["AltGr", "AltGr"]]
    ];
}

// Retorna los caracteres del teclado numérico
// pNumArray: arreglo de caracteres numéricos
// pCharArray: arreglo de caracteres
// pSpecialCharArray: arreglo de caracteres especiales
function zGetNumPadLayout (pNumArray, pCharArray, pSpecialCharArray){
  return [
      [pNumArray.shift(), pNumArray.shift(), pNumArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift() ],
      [pNumArray.shift(), pNumArray.shift(), pNumArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift() ],
      [pNumArray.shift(), pNumArray.shift(), pNumArray.shift(), pNumArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift(), pCharArray.shift() ],
      [["Caps", "Caps"],["Bksp", "Bksp"]]      
    ];
}

// #endregion VirtualKeyboard


// Convierte en mayuscula las letras que  el usuario esta digitando y valida los  caracteres especiales
function validatecontrol(ctrl) {
 
            var t = ctrl.value;
            ctrl.value = t.toUpperCase();
            if (ctrl.value.match(/[^a-zA-Z0-9 .,-@_]/g)) {
                ctrl.value = ctrl.value.replace(/[^a-zA-Z0-9 .,]/g, '');
            } 
        }



// Convierte en mayuscula las letras que  el usuario esta digitando y valida los  caracteres especiales
function validatecontrolMail(ctrl) {
 
            var t = ctrl.value;
            ctrl.value = t.toUpperCase();
            if (ctrl.value.match(/[^a-zA-Z0-9 .,-@_]/g)) {
                ctrl.value = ctrl.value.replace(/[^a-zA-Z0-9 .,-@_]/g, '');
            } 
        }