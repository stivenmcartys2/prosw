var _cleaveFormatId;

var time = new Date(startValue);
var interv;

function startTime() {
    interv = setInterval(function () {
        time = new Date(time - 1000);
        if (time <= 0) {
            clearInterval(interv);
        }
        displayTime();
    }, 1000);
}

function displayTime() {
    jQuery(".time").text(fillZeroes(time.getMinutes()) + ":" + fillZeroes(time.getSeconds()));
}

function fillZeroes(t) {
    t = t + "";
    if (t.length == 1)
        return "0" + t;
    else
        return t;
}

jQuery(document).ready(function () {
    if (jQuery("#cbx") != null) {
        jQuery("input#ctIdDigitalSignature").val("");
        jQuery("#ctTypeIdDigitalSignature :radio:first").prop("checked", true);
    }

    if (document.querySelector(".ctIdDigSig") != null) {
        _cleaveFormatId = new Cleave('.ctIdDigSig', {
            numericOnly: true,
            delimiter: '-',
            blocks: [2, 4, 4]
        });
    }
});

function TypeIdDigSigClick() {
    var idDigSig = jQuery("input#ctIdDigitalSignature");
    idDigSig.val("");
    var checkVal;

    if (_cleaveFormatId != undefined) {
        _cleaveFormatId.destroy();
    }

    var rb = document.getElementById("ctTypeIdDigitalSignature");
    var radio = rb.getElementsByTagName("input");
    for (var i = 0; i < radio.length; i++) {
        if (radio[i].checked) {
            checkVal = radio[i].value;
            break;
        }
    }

    if (checkVal === "N") {
        _cleaveFormatId = new Cleave('#ctIdDigitalSignature', {
            numericOnly: true,
            delimiter: '-',
            blocks: [2, 4, 4]
        });
        idDigSig[0].placeholder = "00-0000-0000";
    } else {
        _cleaveFormatId = new Cleave('#ctIdDigitalSignature', {
            numericOnly: true,
            delimiter: '',
            blocks: [12]
        });
        idDigSig[0].placeholder = "000000000000";
    }
}

function cbDigitalSignatureOnClick(e) {
    TypeIdDigSigClick();
    if (e) {
        jQuery("#hfDigSigCheck").val(true);
        var vDigSigIDStored = jQuery("#hfDigSigIDStored").val();
        if (vDigSigIDStored == "") {
            jQuery("#tbDigitalSignature").fadeIn();
        } else {
            jQuery("#tbDigitalSignature").hide();
            jQuery("#ctIdDigitalSignature").val(vDigSigIDStored);
        }
        ValidatorEnable(document.getElementById('rvIdDigitalSignature'), true);

        if (jQuery("#OptionsLogin").length) {
            jQuery("#OptionsLogin").hide();
        }
        if (jQuery("#divAuthUC").length) {
            jQuery("#divAuthUC").hide();
        }
    } else {
        jQuery("#hfDigSigCheck").val(false);
        jQuery("#tbDigitalSignature").hide();
        ValidatorEnable(document.getElementById('rvIdDigitalSignature'), false);

        if (jQuery("#OptionsLogin").length) {
            jQuery("#OptionsLogin").fadeIn();
        }        
    }
}

function cbReload() {
    jQuery("#ValidateAlias").fadeIn();
    jQuery("#ctErrorDigitalSig").hide();
}

function AwaitRespDigSig() {
    startTime();
    jQuery("#btAwaitResponseDigitalSignature").click();
    CtlFih("false");
    CtlPrv("false");
}

function CtlFih(e) {
    if (e === "True") {
        if (jQuery("#FinishButton") != null) {
            jQuery("#FinishButton").show();
        }
        if (jQuery("#ctlPaymentNext") != null) {
            jQuery("#ctlPaymentNext").show();
        }
        if (jQuery("#StepNextButton") != null) {
            jQuery("#StepNextButton").show();
        }
    } else {
        if (jQuery("#FinishButton") != null) {
            jQuery("#FinishButton").hide();
        }
        if (jQuery("#ctlPaymentNext") != null) {
            jQuery("#ctlPaymentNext").hide();
        }
        if (jQuery("#StepNextButton") != null) {
            jQuery("#StepNextButton").hide();
        }
    }
}

function CtlPrv(e) {
    if (e === "True") {
        if (jQuery("#FinishPreviousButton") != null) {
            jQuery("#FinishPreviousButton").show();
        }
        if (jQuery("#ctlPaymentPrevious") != null) {
            jQuery("#ctlPaymentPrevious").show();
        }
        if (jQuery("#StepPreviousButton") != null) {
            jQuery("#StepPreviousButton").show();
        }
    } else {
        if (jQuery("#FinishPreviousButton") != null) {
            jQuery("#FinishPreviousButton").hide();
        }
        if (jQuery("#ctlPaymentPrevious") != null) {
            jQuery("#ctlPaymentPrevious").hide();
        }
        if (jQuery("#StepPreviousButton") != null) {
            jQuery("#StepPreviousButton").hide();
        }
    }
}

function ShowBtnBack() {
    jQuery("#divBtnBack").fadeIn();
}

function ShowProfileDigSig() {
    jQuery("#btShowProfileDigSig").click();
}

function IdDigSigKeyUp(e) {
    var typeId = jQuery("#ctTypeIdDigitalSignature input:checked").val();
    var valPress = e.value;
    if ((valPress.length > 1) && (valPress.startsWith("0") == false) && (typeId === "N")) {
        e.value = "";
    }
    if ((valPress.length > 1) && (valPress.startsWith("5") == false) && (valPress.startsWith("1") == false) && (typeId === "E")) {
        this.value = "";
    }
    if ((valPress.length == 1) && (valPress != "0") && (typeId === "N")) {
        e.value = "0" + valPress;
    }
    if ((valPress.length == 1) && (valPress != "5") && (valPress != "1") && (typeId === "E")) {
        e.value = "";
    }
}

function ShowHidecbAuth(e) {
    if (e == "True") {
        jQuery("#divBtnAuth").fadeIn();
    } else {
        jQuery("#divBtnAuth").hide();
    }
}

function SetCbx(e) {
    if (e == "True") {
        jQuery("#cbx").prop('checked', true);
    } else {
        jQuery("#cbx").prop('checked', false);
    }
}

function ShowHideAllControls(e) {
    if (e) {
        jQuery("#divContainAllControls").fadeIn();
    } else {
        jQuery("#divContainAllControls").hide();
    }
}

function cbAuth_click() {
    var id = jQuery("input#ctIdDigitalSignature").val();
    var digSigIDStored = jQuery("#hfDigSigIDStored").val();
    if (id === "" && digSigIDStored === "") {        
        hideLoading();
        return false;
    } else {
        ShowHidecbAuth("False");
        showLoading();
        return true;
    }
}

function copyToClipboard(element) {    
    try {
        jQuery('#' + element).each(function () {
            var textVal = (jQuery.trim(jQuery(this).text()).split(' '));            
            var $temp = jQuery("<input>");
            jQuery("body").append($temp);
            $temp.val(textVal[0]).select();
            document.execCommand("copy");
            $temp.remove();
            jQuery("#lblInfoCopy").css('visibility', 'visible');
            setTimeout(function () {
                jQuery("#lblInfoCopy").fadeOut('fast', function () {
                    jQuery("#lblInfoCopy").css("visibility", "hidden");
                    jQuery("#lblInfoCopy").css("display", "inline-block");
                });
            }, 2000);
        });
    }
    catch (e) {
        console.log(e);
    }
}