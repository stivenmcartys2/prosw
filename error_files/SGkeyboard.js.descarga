function AsignaValor(Nombre,Valor,LongitudMax){
    var Campo = document.getElementById(Nombre);
    var largo = Campo.value.length;

    if (largo < LongitudMax || LongitudMax == undefined) {
        if (Valor == "") {
            Campo.value = "";
        } else {
            if (Campo.value != "") {
                Campo.value = Campo.value + Valor;
            } else {
                Campo.value = Valor;
            }
        }
    }
}

function randOrd(){
    return (Math.round(Math.random())-0.5);
}

function marcador(Div,Nombre,longitudMax){
    var resultado = "";
    var num  = new Array('1','2','3','4','5','6','7','8','9','0');
    num.sort(randOrd);
    resultado = "<table cellpadding='1' cellspacing='3' width='70'>";
    var ini = 0;
    var fin = 3;
    var longMax = 50; //tamano por defecto cuando no se asigna longitudMax para el control

    if (arguments.length == 3 && arguments[2] != undefined) {
        longMax = longitudMax;
    }

    resultado += "<tr bgcolor='#F0F7FD'>";            
    for (var i=0; i<4; ++i) { //filas
        for ( var n=ini; n<fin; ++n ){
         if (num[n] != undefined) {
             resultado += "<td align='center'><input type='button' onclick=\"AsignaValor('" + Nombre + "','" + num[n] + "','" + longMax + "')\" value=" + num[n] + " class='button_key'></td>";
         }
        }
        if (n<9){
         ini = n;
         fin = ini + 3;
        }else if (n==9){
         ini = n;
         fin = ini + 6;
        }else if(n==15){
            resultado += "<td colspan='2' align='center' style='cursor:pointer;' onclick=\"AsignaValor('"+Nombre+
            "','')\" class='BtnClear'><strong>Limpiar</strong></td>";
        }
        resultado += "</tr>";
    }
    
    resultado += "</table>";
    document.getElementById(Div).innerHTML=resultado;
}