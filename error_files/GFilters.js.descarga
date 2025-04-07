//#region Documentation
// History
// v4.0.18.0 victor.viquez - SGAL - 01_Octubre_2013 
//           - Se agrega funcionalidad para que el zOnPreinit pueda navegar a una Url externa, ya sea con http o https.
//           - Modificación para validar Firefox ya que al presionar dos veces seguidas el boton que invoca el llamado cancela el postback.  
// v4.0.10.0 dorian.rovira - SGAL - 21_Noviembre_2008
//           Creación.
//#endregion Documentation
//Verifica si los popups están bloqueados
function zIsPopupBlocked(){
   var vWindow = window.open('','','width=1,height=1,left=0,top=0,scrollbars=no');
   if(vWindow){
      var vPopUpsBlocked = false
      vWindow.close()
   }
   else
      var vPopUpsBlocked = true

   return vPopUpsBlocked
}

//#region Documentation
// History
// v4.0.10.0 marcial.bermudez - SGAL - 20_NOviembre_2008
//           Creación.
//#endregion Documentation
//Bloqueo del ENTER en la aplicacion web
function zEnterLock(e) {
   whichkey = (window.event)? event.keyCode: e.which;
                         
    if (whichkey==13) {
      return false;
   }
}

//#region Documentation
// History
// vHB2 mainor.mora - SGAL - 25_Agosto_2011
//      Caso#36460 - Se quita la validación a nivel de versiones que existia, solamente se validará que sean
//                   los navegadores Internet Explorer, FireFox, Chrome y Safari. Se se coloca una validación de una versión mínima para cada navegador.
// v4.0.11.8 armando.chavarria SGAL 10_Junio_2011
//	     Se ajusta la validación del Mobile y se usa el string de mobile
// v4.0.11.7 armando.chavarria SGAL 09_Junio_2011
//	     Se crea nuevamente la función validando el motor del navegador y no versión digital.
// v4.0.11.6 roger.diaz - SGAL - 19_Mayo_2009
//           Se habilita el uso de ie8
// v4.0.10.0 dorian.rovira - SGAL - 14_Noviembre_2008
//           Creación.
//#endregion Documentation
//Verifica los exploradores válidos y su respectiva versión.  En caso de que no sea válido
//retorna la versión utilizada.
function zValidateBrowser(){
  var vIsValid = false; //Variable para indicar si se permitira el acceso al navegador

  var isApplWebKit = navigator.userAgent.indexOf('AppleWebKit'); //Variable que indica si el navegador usa el motor AppleWebKit
  var isLikeGecko = navigator.userAgent.indexOf('like Gecko'); //Variable que indica si el navegador referencia al motor Gecko
  var isGecko = navigator.userAgent.indexOf('Gecko'); //Variable que indica si el navegador usa el motor Gecko
  var isVersion = 0;  
  
  if (isApplWebKit == -1 && isLikeGecko == -1){ //Valida si el navegador no usa estos tipos
    if (isGecko > 1){ //Mozilla Firefox
      var ua      = navigator.userAgent.toLowerCase();
      var rvStart = ua.indexOf('rv:');                  
      var rvEnd   = ua.indexOf(')', rvStart);           
      isVersion   = (ua.substring(rvStart+3, rvEnd)).substring(0,3);
      if (isVersion >= 1.8){ //Valida la versión sea la 2.0 o posterior. Acá se modifica para futuras versiones
        vIsValid = true;
      }
    } else { //Microsoft Internet Explorer
      isVersion = navigator.appVersion;
      isVersion.match(/(MSIE)(\s*)([0-9].[0-9]+)/ig);
      isVersion = RegExp.$3;
      if (isVersion >= 6.0){ //Valida la versión sea mayor o igual a 6.  Acá se modifica para futuras versiones
         vIsValid = true;
      }
    }
  } else { //Chrome y/o Safari
    var ua      = navigator.userAgent.toLowerCase();
    var rvStart = ua.indexOf('applewebkit/');
    var vstart = ua.indexOf('AppleWebKit/');
    var rvMobile = ua.indexOf('mobile/');
    var rmobile = ua.indexOf('Mobile/');
    var rvEnd   = ua.indexOf('(', rvStart);
    isVersion   = (ua.substring(rvStart+12, rvEnd)).substring(0,3);
    isversionM  = (ua.substring(vstart+12, rvEnd)).substring(0,3);
    if (isVersion >= 533){ //Valida la versión sea mayor a 4.  Acá se modifica para futuras versiones
      vIsValid = true;
    }
    
    if ((rvMobile == -1) || (rmobile == -1)){
      if (isVersion >= 531){ //Valida la versión dentro de un rango.  Acá se modifica para futuras versiones
        vIsValid = true;
      }
    }
  }

  //Se valida para que no se pueda entrar con dispositivos móviles de mac --Se conserva apartir de acá
  // if((navigator.userAgent.match(/iPhone/i)) ||
  //    (navigator.userAgent.match(/iPod/i)) ||
  //    (navigator.userAgent.match(/iPad/i))
  //   ){
  //   vIsValid = false
  // }
   if (!vIsValid){
      return navigator.userAgent
   }else{
      return ''
   }
}


//#region Documentation
// History
// v4.0.13.0 mainor.mora - SGAL - 16_Agosto_2011
//      Caso#36460 - Se quita la validación a nivel de versiones, solamente se validará que sean
//                   los navegadores Internet Explorer, FireFox, Chrome y Safari
// v4.0.11.7 luis.esquivel - SGAL - 15_Marzo_2010
//           Caso#23949 - Se habilita el uso de ff3.6
// v4.0.11.6 roger.diaz - SGAL - 19_Mayo_2009
//           Creación.
//#endregion Documentation
//Retorna los exploradores válidos y su respectiva versión.
function zGetCertifiedBrowserNames(pBrowser, pSeparator){
  var vBrowsers  = '';
  if(pBrowser=='all'){
    vBrowsers  =  'Internet Explorer' + pSeparator + 'Firefox' + pSeparator+
                  'Safari' + pSeparator + 'Chrome' + pSeparator;
  }else if(pBrowser=='ie'){
    vBrowsers  = 'Internet Explorer';
  }else if(pBrowser=='ff'){
    vBrowsers  = 'Firefox';
  }else if(pBrowser=='sf'){
    vBrowsers  = 'Safari';
  }else if(pBrowser=='ch'){
    vBrowsers  = 'Chrome';
  }
  return vBrowsers;
}


//#region Documentation
// History
// v0.0.0.1 marcial.bermudez - SGAL - 30_Junio_2008
//          Creación.
//          Invoca un PostBack a la página enviando un eventTarget fijo (GoToPage) y como eventArgument la página hacia dónde se va a navegar
//          Esta funcionalidad aplica solo para los menues que son configurados por medio de un Web.sitemap.
//#endregion Documentation
function zOnPreInit(pURL)
{
    var vBackDiv = document.getElementById("BackDiv");
    var vLoadingDiv = document.getElementById("LoadingDiv");
    var isValid = false;
    if (vBackDiv != null && vLoadingDiv != null) {
        vBackDiv.style.display = "block";
        vBackDiv.style.zIndex = "1000000";
        vLoadingDiv.style.display = "block";
        window.onscroll = function() {
            document.getElementById("BackDiv").style.top = document.documentElement.scrollTop ? document.documentElement.scrollTop : document.body.scrollTop
        };
        var vTop = document.documentElement.scrollTop ? document.documentElement.scrollTop : document.body.scrollTop;
        document.getElementById("BackDiv").style.top = vTop
    } 
    vNewUrl = '';
    if(pURL.indexOf('https=') != -1 ){
      vNewUrl = pURL.replace('https=','https://');
      window.open(vNewUrl);
    }
    else
    {
       if(pURL.indexOf('http=') != -1 ){
          vNewUrl = pURL.replace('http=','http://');
          window.open(vNewUrl);
       } 
       else {
            __doPostBack('GoTo', pURL);
       } 
    }    

  //Modificación para validar Firefox ya que al presionar dos veces seguidas el boton que invoca el llamado cancela el postback.  
  if(navigator.userAgent.search('Firefox') == -1)
        return false;
 
}
//#region Documentation
// History
// v4.0.13.0 jose.vasquez - SGAL - 03_Octubre_2011
//          Creación.
//          Abre una ventana en forma de popup
//          Esta funcionalidad aplica solo para los menues que son configurados por medio de un Web.sitemap.
//#endregion Documentation
function zOnPopup(pWindow,pURL,pFeatures,pOpenType)
{
  pWindow.open(pURL,pOpenType,pFeatures);  
}

//#region Documentation
// History
// v0.0.0.1 marcial.bermudez - SGAL - 30_Junio_2008
//          Creación.
//          Cambia el atributo "display" del elemento "zContent"
//          Se utiliza para validar que JavaScript esté habilitado en el Explorador de Internet
//#endregion Documentation
function zInit() {
  document.getElementById('zContent').style.display = 'block';
  zNoFrames();
}
//#region Documentation
// History
// v0.0.0.3 marcial.bermudez - SGAL - 22_Octubre_2008
//          Se verifica si hay error para luego redireccionar. Ya no se verifica el código de error ya que FF no funcionaba.
// v0.0.0.2 marcial.bermudez - SGAL - 31_Julio_2008
//          Actualización para permitir que la página sea consumida por frames que están en el mismo servidor
// v0.0.0.1 marcial.bermudez - SGAL - 30_Junio_2008
//          Creación.
//          Cambia la localización de una página cuando la misma es invocada desde un frame.
//#endregion Documentation
function zNoFrames() {
  var vHost =""
  if (top != self)
  {
    try
    {
       vHost = top.location.hostname;
    }
    catch (err)
    {
       top.location = self.location;
    }
  }
}

function zSetSecureNavigation() {
  var result = "";
  var httpRequest;

  if( typeof XMLHttpRequest == "undefined" ) {
    XMLHttpRequest = function() {
                                  try { return new ActiveXObject("Msxml2.XMLHTTP.6.0") } catch(e) {}
                                  try { return new ActiveXObject("Msxml2.XMLHTTP.3.0") } catch(e) {}
                                  try { return new ActiveXObject("Msxml2.XMLHTTP") } catch(e) {}
                                  try { return new ActiveXObject("Microsoft.XMLHTTP") } catch(e) {}
                                  throw new Error( "This browser does not support XMLHttpRequest." )
                                };
    httpRequest = XMLHttpRequest();
  } else {
    httpRequest = new XMLHttpRequest();
  }



  httpRequest.open('GET', 'Galileo.GlobalNetCommon.UI.Web/scripts/ASP/SecureNavigate.asp?v='+ Math.random(), false);
  httpRequest.send(null); // this blocks as request is synchronous

  try {
      if (httpRequest.status == 200) {
        if (httpRequest.responseText == "true") {
          result = "";
        } else {
          result = "SETTING_ERROR";
        }
      } else {
        result = "NETWORK_ERROR";
      }
    } catch (e) {
      result = "STATUS_ERROR";
    }
    return result;
}


//#region Documentation
// History
// v4.0.10.2 saheed.chavarria - SGAL - 03_Noviembre_2008
//           Se modifica para que se ejecute el ASP desde el SRC de un objeto image.
//           Al hacerlo de esa manera se elimina el PopUp
// v4.0.10.1 marcial.bermudez - SGAL - 28_Octubre_2008
//           Se modifica para que el mismo sea quien cierre la ventana que abre.
// v4.0.10.0 marcial.bermudez - SGAL - 22_Octubre_2008
//           Creación.
//#endregion Documentation
//Permite nevegacion segura
function zNavigate() {

    var navigationResult = zSetSecureNavigation();

    if (navigationResult == "NETWORK_ERROR") {
      navigationResult = zSetSecureNavigation();
      if (navigationResult == "NETWORK_ERROR") {
        navigationResult = zSetSecureNavigation();
        if (navigationResult == "NETWORK_ERROR") {
          alert("No se puede navegar por problemas de red");
        }
      }
    } else {
      if (navigationResult == "SETTING_ERROR") {
        alert("Hay problemas en servidor web");
      }
      if (navigationResult == "STATUS_ERROR") {
        alert("Pueden haber problemas por su navegador ");
      }
    }
}

//#region Documentation
// History
// v4.0.10.0 dorian.rovira - SGAL - 31_Octubre_2008
//           Creación.
//#endregion Documentation
//Verifica si el contenido contempla únicamente los caracteres listados:
// [ ABCDEFGHIJKLMNOPQRSTSVWXYZ!"#$%&'()*+,-./1234567890 ]
//La evaluación es restrictiva, de modo que el contenido debe tener al menos un
//elemento de cada grupo: Letras + Números + Símbolos, sin importar el orden.
function zValidatePassword(pPassword)
{
    var vRegExp = new RegExp("\w*([a-zA-Z_0-9]*[#$%&'()*+,-./])");
    return vRegExp.exec(pPassword);
}